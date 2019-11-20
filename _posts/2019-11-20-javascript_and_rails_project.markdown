---
layout: post
title:      "**"# JavaScript and Rails Project" "
date:       2019-11-20 22:15:29 +0000
permalink:  javascript_and_rails_project
---


Completing my JavaScript and Rails project was a challenge for me, but enjoyable as I learned a lot from the process. The most helpful thing I took away from the project was the ability to use fetch to make requests with the server and persist my changes, like adding new homework, checking homework off as complete or deleting homework. 

My Homework class was to render the following:
```
   render() {
        return `
        <div id="${this.id}" class="card">
            <div class="card-content">
                <h2>${this.subject.name}</h2>
                <p>${this.content} </p>
                <p>Due: ${this.date}</p>
                <p>Complete? <input id="complete-${this.id}" onclick="completedHomework(${this.id})" type="checkbox" ${this.checked}/></p>
            </div>
            <button onclick="deleteHomework(${this.id})">Delete</button>
        </div>
        `
    }
```
 
It is important that the div element is id’ed with the instance’s id as when we try and delete it we must know what homework we are talking about. 

For my deleteHomework function I firstly found the div element by it’s id and called .remove() on it to get rid of it. 

function deleteHomework(id) {
    document.getElementById(`${id}`).remove()
}

Then I needed to persist this to the server by using fetch to change to json object. 
```

fetch(`http://localhost:3000/homeworks/${id}`, {
        method: 'DELETE',
        headers: {
            'Content-Type' : 'application/json'
        }
    })
```

Fetch takes in 2 parameters the url or filename of the place where the data is stored and an option object which can include methods, headers, body and mode. In this case the URL passed in is the RESTful URL of “homeworks/${id}”. The option object includes the method, which is of course “DELETE” and the header to change, 'Content-Type' : 'application/json'.  This means that the only type of file that I am willing to accept is a json file. No my delete request will persist! 


