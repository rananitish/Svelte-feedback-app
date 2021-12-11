<script>
 import {v4 as uuidv4} from 'uuid';
import Button from "./Button.svelte";
import {createEventDispatcher} from 'svelte';
import Card from "./Card.svelte";
import RatingSelect from "./RatingSelect.svelte";

const dispatch=createEventDispatcher();
let feedback=" ";
let rating=10;
let btnDisabled=false;
let min=10;
let message;

const handleInput=( )=>{
    if(feedback.trim().length<=min){

        message=`Text must be at least ${min} char`;
        btnDisabled=true;
    }
    else{
        message=null;
        btnDisabled=false;
    }
}

const handleSelect=(e)=>{
 rating=e.detail;
}

const handleSubmit=()=>{
    if(feedback.trim().length>=min){

        const newFeedback={
            id:uuidv4(),
            feedback,
            rating:+rating
        }
        dispatch('add-fb',newFeedback);
        feedback=' ';
    }
}
</script>
<Card>

    <header>
        <h2>How would you rate your service with us</h2>
    </header>
<form on:submit|preventDefault={handleSubmit}>
    
    <div class="input-group">
        <input type="text" on:input={handleInput} bind:value={feedback} placeholder="Write Ur Reviews" />
        <Button disabled={btnDisabled} type="submit" >Send </Button>
    </div>
    <RatingSelect on:rating-select={handleSelect} />
    {#if message}

     <div class="message">{message}</div>
    {/if}

 
</form>


</Card>



<style>
  header {
    max-width: 400px;
    margin: auto;
  }
  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }
  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }
  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }
  input:focus {
    outline: none;
  }
  .message{
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
