<script>
import Moveable from "svelte-moveable";

let targetRef = null;
const list = [
  [
    ['MyDesk', 78, 44],
    ['もくもく', 68, 23],
    ['全社', 47, 28],
    ['Event', 36, 17],
  ],
  [
    ['MTG1', 50, 16],
    ['MTG2', 55, 16],
    ['MTG3', 60, 16],
    ['MTG4', 65, 16],
  ],
  [
    ['1-1', 78, 34],
    ['1-2', 74, 34],
    ['1-3', 76, 31],
    ['1-4', 72, 31],
    ['1-5', 78, 23],
    ['1-6', 74, 23],
  ],
]

const teleport = ({ x, y }) => {
  const mapId = window.game.getMyPlayer().map;
  window.game.teleport(mapId, x, y);
};
const style = document.createElement('style');
style.textContent = ".moveable-line { display: none; }";
document.head.appendChild(style);
</script>

<div style="z-index: 1;">
  <div>
    <div
      style="
        position: absolute;
        width: 300px;
        text-align: center;
        box-sizing: border-box;
        background-color: rgba(32,37,64, 0.4);
        border: 1px solid #202540;
      "
      bind:this={targetRef}
    >
      {#each list as row}
        <div style="display: flex;">
          {#each row as [name, x, y] }
            <button
              style="
                flex-grow: 1;
                font: inherit;
                background-color: rgba(32,37,64, 0.9);
                color: white;
                font-family: 'DM Sans', sans-serif;
              "
              on:click={() => {teleport({ x, y })} }
            >
              {name}
            </button>
          {/each }
        </div>
      {/each }
    </div>

    <Moveable
      origin={false}
      target={targetRef}
      className="moveable"
      draggable={true}
      throttleDrag={1}
      edgeDraggable={false}
      startDragRotate={0}
      throttleDragRotate={0}
      on:drag={({ detail: e }) => {
          e.target.style.transform = e.transform;
      }}
    />
  </div>
</div>
