<template>
<div>
    <slot>
  <ul>
        <li v-for="(media,i) in mediaList" :key="i"> 
{{media.mediaDescription}}
        </li>
    </ul>
    </slot>
  
 
</div>
  
</template>

<script>
export default {
    data(){
        return {
             mediaList: [
        {
          mediaID: "video43",
          mediaName: "BC_welcome_video",
          mediaSource: "",
          mediaType: "video",
          mediaDescription: "What will you discover at Melaleuca",
          mediaTag: "",
          mediaThumbnail:
            "/Images/BusinessCenter/Landing_Page/getting-started/thumbs/foundations-a.jpg",
        },
        {
          mediaID: "video150",
          mediaName: "gs_frank_message_2020",
          mediaSource: "",
          mediaType: "video",
          mediaDescription:
            "First truly natural company of any size, and we're the only ones left. - Frank VanderSloot, CEO",
          mediaTag: "",
          mediaThumbnail:
            "/Images/BusinessCenter/Landing_Page/getting-started/thumbs/bg--video150.jpg",
        },
        {
          mediaID: "video42",
          mediaName: "BC_convention_values",
          mediaSource: "",
          mediaType: "video",
          mediaDescription:
            "See how Melaleuca provides the freedom for Marketing Executives to live a better life on their own terms",
          mediaTag: "",
          mediaThumbnail:
            "/Images/BusinessCenter/Landing_Page/getting-started/thumbs/melavalues.jpg",
        },]
        }
    }
}
</script>