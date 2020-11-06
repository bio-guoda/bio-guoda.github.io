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
    <option value="inaturalist">inaturalist</option>
</select>
</div>

<p id="status"></p>
<p id="eml"></p>

<p id="websocket"></p>

<script>
  
  let websocket = new WebSocket("wss://echo.websocket.org");
  websocket.onmessage = function (event) {
    console.log(event.data);
  }
  websocket.onopen = function (event) {
    websocket.send("ping"); 
  };


  locateDatasets = function() {
    let specimenId = document.querySelector('#identifier').value; 
    let linkType = document.querySelector('#link-type').value; 
    let oReq = new XMLHttpRequest();
    document.querySelectorAll('.result').forEach(function(elem) { elem.remove() });
    document.querySelector('#eml');
    document.querySelector('#status').textContent = 'locating datasets that contain [' + specimenId + ']...';
    oReq.addEventListener("load", function() {
      document.querySelector('#status').textContent = 'the following datasets contain [' + specimenId + '] of type [' + linkType + ']:';
      let result = document.querySelector('#eml').appendChild(document.createElement('div'));
      result.setAttribute('class', 'result');
      this.responseText.split('\n').forEach(function(link) {
          let elemDiv = result.appendChild(document.createElement('div'));
          let elem = elemDiv.appendChild(document.createElement('a'));
          elem.setAttribute('href', link);
          elem.setAttribute('target', '_blank');
          elem.textContent = link;
      });
    });
    let requestUrl = 'https://preston.guoda.bio/find/' + linkType + '/' + specimenId;
    if (websocket.readyState === websocket.OPEN) {
      // replace with sending follow request to some preston service
      websocket.send('requesting: [' + requestUrl + ']');
    }
    oReq.open('GET', requestUrl);
 
    oReq.send(); 
  }
</script>
