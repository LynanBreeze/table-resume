<script>
  import { resumeData } from "./data";
  
  let data = {
    ...resumeData
  }

  const printPage = async () => {
    window.print();
  };

  const deleteRow = (e, sectionIndex, index)=>{
    e.stopPropagation()
    data.sections[sectionIndex].data = data.sections[sectionIndex].data.filter((item, itemIndex)=>itemIndex !== index)
  }

  const addRow = (sectionIndex)=>{
    data.sections[sectionIndex].data = [...data.sections[sectionIndex].data, ['','']]
  }
</script>

<div class={`content-wrapper`}>
  <div class="content">
    <div class="head">
      <div class="title">CURRICULUM VITAE</div>
      <div class="operations">
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div class="print-btn no-print" on:click={printPage}>
          Print
        </div>
      </div>
    </div>
    <div class="body">
      {#each data.sections as section, sectionIndex}
      <div class="section">
        <!-- svelte-ignore a11y-click-events-have-key-events -->
        <div class="title">{section.title}<div class="add-row-btn no-print" on:click={()=>addRow(sectionIndex)}>+ Add Row</div></div>
        <table class="info-table">
          <tbody>
            {#each section.data as row, index}
            <tr>
              <td contenteditable>{row[0]}</td>
              <!-- svelte-ignore a11y-click-events-have-key-events -->
              <td contenteditable>{row[1]}<div contenteditable="false" class="delete-btn" on:click={(e)=>deleteRow(e, sectionIndex, index)}>X</div></td>
            </tr>
            {/each}
          </tbody>
        </table>
      </div>
      {/each}
    </div>
  </div>
</div>
