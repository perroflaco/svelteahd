<script>
 import { Accordion, AccordionItem } from 'svelte-collapsible'
 let reponse={}
 let id=0
 let proceso=''
 let nivel=''
 let mensaje=''
 let fecha=''
 let historial=[]

 $: fetch('http://localhost:3000/procesos/1')
    .then(res=>res.json())
    .then(apiResponse=>{
        reponse=apiResponse.Mensaje
        id=apiResponse.id
        proceso=apiResponse.proceso
        nivel=apiResponse.nivel
        mensaje=apiResponse.mensaje
        fecha=apiResponse.fecha
        historial= apiResponse.historial
    
    })
</script>
<h1>{proceso}</h1>
<h2>{nivel}</h2>
<div>{fecha}</div>
<div>{mensaje}</div>
<ul>
{#each historial as {mensaje,fecha,index} }
    <Accordion>
        <AccordionItem key='index'>
            <h2 slot='header'>{fecha}</h2>
            <p slot='body'>{mensaje}</p> 
        </AccordionItem>
    </Accordion>
{/each}
</ul>