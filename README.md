# Animations-With-React-Hooks

Everyone loves a fun animation to get some feedback that the action your attempting was successful. A UI can become much more engaging and comfortable with the right animations. This past week I was looking to give an app i'm working on a little more spunk and life by adding in some animations after a response from the api comes back, and the props passed down are changed. I also wanted to give [React Hooks](https://reactjs.org/docs/hooks-intro.html) a try since hooks allow function components to manage state(Which is awesome!).

### Component
Let us begin by creating a basic function component -- 
```
#useState and useEffect are the hooks we will be using
import React, { useState, useEffect} from 'react'
import 'example.css'


export default function(props) {

# we can declare a state variable with the following syntax
  const [itemCheck, setItemCheck] = useState(props.item.checked)
  const [animateItem, setAnimateItem] = useState("")
  
    #useEffect tells React our component needs to do something after render
    useEffect(() => {
        setItemCheck(props.item.checked)
        props.item.checked ? setAnimateItem("animated example") : setAnimateItem("")
    })
    
    
  return (
    <div className="clickable" onClick={() => props.checkItem(props.list.id, props.item.id)}>   #checkItem() is our api request
      {itemCheck &&
             # &#10003; is the UTF-8 decimal reference for a check mark!
        <div className={animateItem}}>&#10003;</div>
      }
    </div>
    
  )
}
```
To break this down a little bit we have a function component using React Hooks useState useEffect to set and alter the state. We have a prop handed down called item which has an attribute of checked(boolean). We have another prop called checkItem() which is a function that makes a request to the api to update the item. `checkitem()` is called when we click on the div with the className 'clickable'. When our api request comes back with the changed data of checked === true useEffect will be called which will call setAnimateItem() changing the state to 'animated example'. `itemCheck` will be true(ln 29) and will return the `div` with the checkmark. Now all thats left to do is write some css!!

### The CSS
Now we will add the final touches with a little style!
```
.clickable {
  border-style: solid;
}

.animated {
    -webkit-animation-duration: 0.5s;
    -webkit-animation-fill-mode: both;
    animation-duration: 0.5s;
    animation-fill-mode: both;
} 


.example {
  width: 1.5em;
  height: 1.5em;
  
  border-radius: 50%;
  -webkit-animation-name: example;
  animation-name: example;
}



 @keyframes example {
  from{transform:scale(0)}
  80%{transform:scale(1.5)}
  to{transform:scale(1)}
}

@-webkit-keyframes example {
  from{-webkit-transform:scale(0)}
  80%{-webkit-transform:scale(1.5)}
  to{-webkit-transform:scale(1)}
}
```
This will give us a pulse effect when the inner `div` renders. I look forward to more projects using React Hooks and animation! I recommend you check out the documentation and start using hooks if you haven't already.
