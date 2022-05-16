<script>
    
    import {page} from '$app/stores';
    import { ImageLoader, 
      Button,
       Tile,
       Grid, 
       Row,
      Column,
      Tag, 
Content} from "carbon-components-svelte";
    import { onMount} from "svelte";


    /**
* @type {any[]}
*/
    let artWorks = [];

    onMount(async () => {
        var searched = $page.params.searched;
        const sketchfabArt =await fetch (`https://api.sketchfab.com/v3/search?type=models&q=${searched}&user=sferagallery&archives_flavours=false`)
        var res = await sketchfabArt.json();
        artWorks = res.results;
        console.log(artWorks)
    });
    </script>
    
    <section>
      <Grid 
     
      noGutter='true'
      padding='true'
      >
      <Row
      noGutter='true'
      
      >
          
            {#each artWorks as artWork}
           
            <Column
            noGutter='true'
            sm={8} md={8} lg={8}
            >
            <div class='card'>
             <Tile><h4>{artWork.name}</h4></Tile> 
            <ImageLoader
            src="{artWork.thumbnails.images[0].url}"
            alt="{artWork.name}"
          />
            <Tile>
            <div class="">
          {#each artWork.tags as tag}
            
         
          <Tag size="sm" type='outline'> {tag.name}</Tag>
          {/each}
        </div>
            </Tile>
            <Tile>
            <div class="button"><a  href="#{artWork.uid}"><Button>3D / AR</Button></a>
            </div>
          </Tile>
          </div>
         
                
              
              
              <div id="{artWork.uid}" class="overlay">
                <div class="popup">
                  <Content>
                  
                  <h2>{artWork.name}</h2>
               
                  
                  <a class="close" href="#{artWork.uid+1}">&times;</a>
                
                     </Content>
                    <div class="sketchfab-embed-wrapper, content"> 
                      <iframe 
                      title="{artWork.name}" 
                      frameborder="0" 
                      width="100%"
                      height="500px"
                      allowfullscreen mozAllowFullScreen="true" webkitallowfullscreen="true" 
                      allow="autoplay; fullscreen; xr-spatial-tracking" 
                      xr-spatial-tracking execution-while-out-of-viewport execution-while-not-rendered web-share 
                      src="https://sketchfab.com/models/{artWork.uid}/embed?ui_infos=0&ui_inspector=0&ui_watermark_link=0&ui_stop=0&ui_watermark=0&ui_settings=0&ui_vr=0&ui_annotations=0"> 
                      </iframe> 
                    </div>
                    
                    <p class="descript">
                    {@html artWork.description}
                    </p>
                    </div>
                     
              </div>
            </Column>
            
            {/each}
          </Row>
      </Grid>
         
           
    </section>

    <style> 
    
.card{
  position: relative;
  width: 100%;
  
  border-left: 3px solid #8d8d8d ;
  background-color: #393939;
}


.button{
  
  
  
    }

  
        a {
          text-decoration: none;
        }
        .descript{
          color: #333;
          padding-top: 1em;
        }
        .overlay {
          position: fixed;
          top: 30px;
          bottom: 0;
          left: 0;
          right: 0;
          background: rgba(0, 0, 0, 0.7);
          transition: opacity 500ms;
          visibility: hidden;
          opacity: 0;
          z-index: 1;
        }
        .overlay:target {
          visibility: visible;
          opacity: 1;
        }
  
        
        .popup {
          margin: 20px auto;
          padding: 10px;
          background: #fff;
          border-radius: 0px;
          width: 800px;
          left: 12%;
          position: relative;
          transition: all 0.7s ease-in-out;
          overflow: scroll;
        }
        
        .popup h2 {
          margin-top: 0;
          color: #333;
          font-family: Tahoma, Arial, sans-serif;
        }
        .popup .close {
          position: absolute;
          top: 20px;
          right: 30px;
          transition: all 200ms;
          font-size: 30px;
          font-weight: bold;
          text-decoration: none;
          color: #333;
        }
        .popup .close:hover {
          color: #0f62fe;
        }
        .popup .content {
          
          max-height: 900px;
          
        }
      
       
        
        @media screen and (max-width: 1056px){
         
          .overlay{
            left: 0;
          }
          .popup{
            left: 0px;
            width: 100%;
            height: 100%;
          }
        }
        
            </style>