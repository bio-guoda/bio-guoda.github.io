---
layout: default
title: "registry"
---
<div>
<input type="text" id="identifier" style="width: 50em" value="http://arctos.database.museum/guid/UAM:Herb:74954">
</div>
<button onclick="locateDatasets()" type="button" style="width: 50em; height: 10em; background: yellow">find related datasets</button>

<p id="status"></p>
<p id="eml"></p>

<script>
   
  locateDatasets = function() {
    let specimenId = document.querySelector('#identifier').value; 
    let oReq = new XMLHttpRequest();
    document.querySelector('#status').textContent = 'locating datasets that contain [' + specimenId + ']...';
    oReq.addEventListener("load", function() {
      document.querySelector('#status').textContent = 'the following datasets contain [' + specimenId + ']:';
      document.querySelector('#eml').textContent = this.responseText;
    });
    oReq.open('GET', 'https://preston.guoda.bio/find/arctos/' + specimenId);
    oReq.send(); 
  }
</script>
