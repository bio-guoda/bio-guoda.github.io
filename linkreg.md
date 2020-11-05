---
layout: default
title: "registry"
---
<div>
<button onclick="locateDatasets()" type="button" style="background: yellow">find</button>
<input type="text" id="identifier" style="width: 50em" value="http://arctos.database.museum/guid/UAM:Herb:74954">
</div>

<p id="status"></p>
<p id="eml"></p>

<script>
   
  locateDatasets = function() {
    let specimenId = document.querySelector('#identifier').value; 
    let oReq = new XMLHttpRequest();
    document.querySelector('#status').textContent = 'locating datasets that contain [' + specimenId + ']...';
    oReq.addEventListener("load", function() {
      document.querySelector('#status').textContent = 'the following datasets contain [' + specimenId + ']:';
      this.responseText.split('\n').forEach(function(link) {
          let elemDiv = document.querySelector('#eml').appendChild(document.createElement('div'));
          let elem = elemDiv.appendChild(document.createElement('a'));
          elem.setAttribute('href', link);
          elem.setAttribute('target', '_blank');
          elem.textContent = link;
      });
    });
    oReq.open('GET', 'https://preston.guoda.bio/find/arctos/' + specimenId);
    oReq.send(); 
  }
</script>
