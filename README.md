# Magic-Notes-app-with-JS

HTML 

<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Notes App</title>



</head>

<body>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x" crossorigin="anonymous">

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Magic Notes</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page" href="#">Home</a>
                    </li>


                </ul>
                <form class="d-flex">
                    <input class="form-control me-2" type="search"  id = 'searchTxt' placeholder="Search" aria-label="Search">
                    <button class="btn btn-outline-success" type="submit">Search</button>
                </form>
            </div>
        </div>
    </nav>

    <div class="container my-4">

        <h2 class="text-center"> Welcome to the Magic Notes </h2>


        <div class="card">

            <div class="card-body">
                <h5 class="card-title">Add a Note</h5>
                <p class="card-text"></p>
                <div class="mb-3">
                    <label for="exampleFormControlTextarea1" class="form-label">Write down your valuable notes down
                        below</label>
                    <textarea class="form-control" id="addTxt" rows="3"></textarea>
                </div>
                <button class="btn btn-primary" id='addBtn'>Add note</button>
            </div>
        </div>

        <h2>Your Notes</h2>
        <hr>
        <div id="notes" class="row container-fluid">
            <div class="my-2 mx-2 card"style="width: 18rem;">

                <div class="card-body">
                    <h5 class="card-title">Note </h5>
                    <p class="card-text"></p>
                    <button class="btn btn-primary">Delete</button>
                </div>

            </div>



        </div>





    </div>














    <script src="notesapp.js"></script>





    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js"
        integrity="sha384-W8fXfP3gkOKtndU4JGtKDvXbO53Wy8SZCQHczT5FMiiqmQfUpWbYdTil/SxwZgAN"
        crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/js/bootstrap.min.js"
        integrity="sha384-skAcpIdS7UcVUC05LJ9Dxay8AXcDYfBJqt1CJ85S/CFujBsIzCIv+l9liuYLaMQ/"
        crossorigin="anonymous"></script>








        




    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.1/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-/bQdsTh/da6pkI1MST/rWKFNjaCP5gBSY4sEBT38Q/9RBh9AH40zEOg7Hlq2THRZ"
        crossorigin="anonymous"></script>
</body>

</html>




Javascript



console.log('Welcome to the Notes App!!!');

// if user adds a note, add it to the localStorage
showNotes()
let addBtn = document.getElementById('addBtn') 

addBtn.addEventListener('click',function(e)    
{

    let addTxt = document.getElementById('addTxt')  
    let notes = localStorage.getItem('notes')  
    if (notes == null)                 
    {
        notesObj = [];    
              
    }
 else
 {
     notesObj = JSON.parse(notes)        
 }
 notesObj.push(addTxt.value)    

 localStorage.setItem('notes',JSON.stringify(notesObj))  
 addTxt.value = '';
 
 showNotes();
})



function showNotes(){
    let notes = localStorage.getItem('notes')
     if (notes == null)
     {
         notesObj = [];
     }
     else 
    {
        notesObj = JSON.parse(notes);

    }

    
    let html = "";
    notesObj.forEach(function(element ,index) {
        
        
        html += ` <div class="my-2 mx-2 card" style="width: 18rem;">

        <div class="card-body">
            <h5 class="card-title">Notes ${index +1}</h5>
            <p class="card-text">${element}</p>
            <button id = "${index} " onclick = 'deleteNote(this.id)' class="btn btn-primary">Delete</button>
        </div>
       
    </div> `;
        
});
let notesElm = document.getElementById('notes')

if ( notesObj.length != 0)
{
notesElm.innerHTML = html;
}

else 
 {
     notesElm.innerText = `Nothing to Show Please use "Add note" to add Notes!!!`
 }
}

//function for deleting a note

function deleteNote(index)
{   
    // console.log("I am deleting!!!",index)

    let notes = localStorage.getItem('notes')
    if (notes == null)
    {
        notesObj = [];
    }
    else  
    {
        notesObj= JSON.parse(notes)
    }

    notesObj.splice(index,1)

    localStorage.setItem('notes',JSON.stringify(notesObj));
    showNotes();

}

let search = document.getElementById('searchTxt')
search.addEventListener('input',function(e)
{
   let inputVal = search.value
//    console.log("Input event is fired!!!",inputVal);

let noteCards = document.getElementsByClassName('my-2 mx-2 card')
Array.from(noteCards).forEach(function(element)
{
    let cardTxt = element.getElementsByTagName('p')[0];
    console.log(cardTxt)
  if (cardTxt.includes(inputVal))
  {
      element.style.display = 'none'
  }

})


})



