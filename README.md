# AlanAi-ECommerce-React-Web-App
Implemented voice integration in a ECommerce website layout using Alan.ai allowing user to add/remove items from cart, show/close cart and checkout.

### `instructions`
1. Download files and import to IDE 
2. Create an account on https://alan.app/ and signin. 
3. Create voice assistant, click empty project then name the project 
4. Copy and paste the AlanAi script into AlanAi and save it 
5. Click intergration and find your Alan SDK Key
6. Copy and paste your key into AlanAi_Ecommerce/Alan-AI/.env and replace the key 
7. Save file 
8. Run "npm start" in terminal 
9. Allow mic permissions in browser

### `functionalities`

### `AlanAi script`
intent ("(open|view) (the|) cart", p=>{
    p.play({ command:'open-cart' })
})

intent ("close (the|) cart", p=>{
    p.play({ command:'close-cart' })
})

const itemNameSlot = "$(ITEM_NAME red|yellow|blue|orange|green|purple|light gray|dark gray)"
const quantityContext = context(()=> { 
    follow("$(QUANTITY NUMBER)", p=> {
        p.play({command: 'add-item' , payload: { quantity: p.QUANTITY.number,name: p.state.name} })
        p.resolve()
    })
    fallback("Please specifiy how many items you want to add")
}) 

intent (`add (the|) ${itemNameSlot} (item|) to (the|) cart`, p=> {
    p.play("How many would you like to add?")
    p.then(quantityContext, { state: { name: p.ITEM_NAME.value } })
})

intent (`remove (the|) ${itemNameSlot} (item|) to (the|) cart`, p=> {
    p.play({command: 'remove-item', payload: { name: p.ITEM_NAME.value}})
}) 

intent ("(checkout|purchase items)", p=>{
    p.play({ command:'purchase-items' })
})

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.


