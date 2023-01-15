+++
title = "Disable button if input is empty"
date = "2022-09-06"
description = "Disable button if input is empty"
tags = ["web","javascript"]
summary = "Disable button if input is empty"
+++
# JQuery

```html
<button type="submit" class="btn btn-sm btn-primary" disabled>Upload file</button>
```

```Javascript
$('input[type=file]').change(function(){
    if($('input[type=file]').val()==''){
        $('button').attr('disabled',true)
    } 
    else{
      $('button').attr('disabled',false);
    }
})
```

[src](https://stackoverflow.com/a/37226934/6577778)

# Vanilla Javascript

```html
<input placeholder="Enter some text" name="name" id='input'/>
<button id='button' disabled>Réserver</button>
```

```Javascript
let inputElt = document.getElementById('input');
let btn = document.getElementById('button');

inputElt.addEventListener("input", function(){
  btn.disabled = (this.value === '');
})
```
[src](https://stackoverflow.com/a/57477648/6577778)
                    