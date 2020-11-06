---
layout: default
title: "registry"
---
<div>
<button onclick="locateDatasets()" type="button" style="background: yellow">find</button>
<input type="text" id="identifier" style="width: 50em" value="http://arctos.database.museum/guid/UAM:Herb:74954">
<select name="pets" id="link-type">
    <option value="arctos" selected>arctos</option>
    <option value="email">email</option>
    <option value="doi">doi</option>
    <option value="symbiota">symbiota</option>
    <option value="uuid">uuid</option>
</select>
</div>

<p id="status"></p>
<p id="eml"></p>

<script>
   
  locateDatasets = function() {
    let specimenId = document.querySelector('#identifier').value; 
    let linkType = document.querySelector('#link-type').value; 
    let oReq = new XMLHttpRequest();
    let result = document.querySelector('#result');
    if (result) { result.remove(); }
    document.querySelector('#eml');
    document.querySelector('#status').textContent = 'locating datasets that contain [' + specimenId + ']...';
    oReq.addEventListener("load", function() {
      document.querySelector('#status').textContent = 'the following datasets contain [' + specimenId + '] of type [' + linkType + ']:';
      let result = document.querySelector('#eml').appendChild(document.createElement('div'));
      result.setAttribute('id', 'result');
      this.responseText.split('\n').forEach(function(link) {
          let elem = result.appendChild(document.createElement('a'));
          elem.setAttribute('href', link);
          elem.setAttribute('target', '_blank');
          elem.textContent = link;
      });
    });
    oReq.open('GET', 'https://preston.guoda.bio/find/' + linkType + '/' + specimenId);
    oReq.send(); 
  }
</script>
