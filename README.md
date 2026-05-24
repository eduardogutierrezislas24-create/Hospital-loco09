<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Hospital Psiquiatrico VR</title>
    <script src="https://aframe.io/releases/1.4.0/aframe.min.js"></script>
    <style>
      #hud {
        position: absolute;
        top: 20px;
        left: 20px;
        color: #00ff00;
        font-family: monospace;
        font-size: 20px;
        pointer-events: none;
        text-shadow: 0 0 10px #00ff00;
        z-index: 10;
      }
      .item-count {
        display: block;
        margin: 10px 0;
      }
      .timer-bar {
        width: 300px;
        height: 20px;
        background: #333;
        border: 2px solid #00ff00;
        margin: 20px 0;
        position: relative;
      }
      .timer-fill {
        height: 100%;
        background: #00ff00;
        width: 0%;
        transition: width 0.1s linear;
      }
    </style>
    <script>
      // Lógica para caminar automático y controles de mirada
      AFRAME.registerComponent('vrcorredor', {
        init: function () {
          this.objetoEnMano = null;
          this.timer = 0;
          this.itemsRecolectados = 0;
          this.gameOver = false;
          this.objetivo = null;
          
          // Crear indicador de carga visual (retículo)
          this.cursor = document.querySelector('a-cursor');
          
          // Escuchar cuando miramos algo
          this.el.addEventListener('raycaster-intersection', (e) => {
            this.objetivo = e.detail.els[0];
          });
          
          this.el.addEventListener('raycaster-intersection-cleared', () => {
            this.objetivo = null;
            this.timer = 0;
            this.updateHUD();
          });
        },
        tick: function (time, timeDelta) {
          if (this.gameOver) return;
          
          // 1. Caminar automático hacia adelante lento (eje Z negativo)
          var pos = this.el.getAttribute('position');
          pos.z -= 0.02; 
          this.el.setAttribute('position', pos);
          
          // 2. Lógica de interacción por tiempo de mirada
          if (this.objetivo) {
            this.timer += timeDelta;
            var porcentaje = (this.timer / 800) * 100; // 0.8 segundos
            
            // Actualizar barra de carga en HUD
            var timerFill = document.querySelector('.timer-fill');
            if (timerFill) {
              timerFill.style.width = porcentaje + '%';
            }
            
            if (this.timer >= 800) { // 0.8 segundos mirando
              
              // Si es un frasco y tenemos la mano vacía, lo recogemos
              if (this.objetivo.classList.contains('item') && !this.objetoEnMano) {
                this.objetoEnMano = this.objetivo;
                this.itemsRecolectados++;
                this.objetivo.setAttribute('visible', 'false');
                this.addMessage('✓ OBJETO RECOGIDO', '#00ff00');
                this.updateHUD();
              } 
              
              // Si miramos al monstruo y llevamos un objeto, se lo lanzamos
              else if (this.objetivo.id === 'monstruo' && this.objetoEnMano) {
                var monstruo = this.objetivo;
                this.addMessage('✓ LANZADO AL MONSTRUO', '#ffff00');
                
                // Animación rápida de lanzamiento
                this.objetoEnMano.setAttribute('animation', 'property: position; to: 0 0 -15; dur: 300');
                
                setTimeout(() => {
                  this.objetoEnMano = null;
                  this.updateHUD();
                  
                  // Si recogimos los 3 items y los lanzamos todos
                  if (this.itemsRecolectados === 3) {
                    this.addMessage('✓✓✓ ¡VICTORIA! MONSTRUO VENCIDO', '#00ff00');
                    monstruo.parentNode.removeChild(monstruo);
                    this.gameOver = true;
                  }
                }, 300);
              }
              this.timer = 0;
            }
          } else {
            // Resetear barra si no estamos mirando nada
            var timerFill = document.querySelector('.timer-fill');
            if (timerFill) {
              timerFill.style.width = '0%';
            }
          }
        },
        updateHUD: function() {
          var hudElement = document.getElementById('hud');
          if (hudElement) {
            hudElement.innerHTML = `
              <div class="item-count">OBJETOS: ${this.itemsRecolectados}/3</div>
              <div class="item-count" style="color: #ffff00;">EN MANO: ${this.objetoEnMano ? '✓' : '✗'}</div>
              <div class="timer-bar">
                <div class="timer-fill"></div>
              </div>
              <div id="messages" style="color: #00ff00;"></div>
            `;
          }
        },
        addMessage: function(text, color) {
          var messagesDiv = document.getElementById('messages');
          if (messagesDiv) {
            var msg = document.createElement('div');
            msg.textContent = text;
            msg.style.color = color;
            msg.style.marginTop = '10px';
            messagesDiv.appendChild(msg);
            
            // Eliminar mensaje después de 2 segundos
            setTimeout(() => {
              msg.remove();
            }, 2000);
          }
        }
      });
    </script>
  </head>
  <body>
    <div id="hud">
      <div class="item-count">OBJETOS: 0/3</div>
      <div class="item-count" style="color: #ffff00;">EN MANO: ✗</div>
      <div class="timer-bar">
        <div class="timer-fill"></div>
      </div>
    </div>

    <a-scene fog="type: linear; color: #050505; far: 15; near: 1">
      
      <a-assets>
        <a-mixin id="pared" material="color: #2b332b"></a-mixin>
      </a-assets>

      <a-sky color="#050505"></a-sky>

      <a-entity id="jugador" position="0 1.6 0" vrcorredor raycaster="objects: .interactuable; far: 10">
        <a-camera wasd-controls-enabled="false">
          <a-entity light="type: spot; intensity: 3; distance: 15; angle: 35" position="0 0 0"></a-entity>
          <a-cursor color="red" scale="0.5 0.5 0.5"></a-cursor>
          <a-entity id="mano"></a-entity>
        </a-camera>
      </a-entity>

      <!-- Escenario -->
      <a-box position="0 -0.1 -20" scale="5 0.1 50" color="#333"></a-box>
      <a-box position="-2.5 2 -20" scale="0.1 4 50" mixin="pared"></a-box>
      <a-box position="2.5 2 -20" scale="0.1 4 50" mixin="pared"></a-box>
      <a-box position="0 4 -20" scale="5 0.1 50" color="#111"></a-box>

      <!-- Items a recoger -->
      <a-cylinder class="interactuable item" color="cyan" position="-0.8 0.2 -4" radius="0.1" height="0.3"></a-cylinder>
      <a-cylinder class="interactuable item" color="cyan" position="0.5 0.2 -8" radius="0.1" height="0.3"></a-cylinder>
      <a-cylinder class="interactuable item" color="cyan" position="-0.3 0.2 -12" radius="0.1" height="0.3"></a-cylinder>

      <!-- Monstruo final -->
      <a-capsule id="monstruo" class="interactuable" color="black" position="0 1 -18" radius="0.4" height="1.8"></a-capsule>

    </a-scene>
  </body>
</html>
