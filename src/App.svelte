<script>
import FeedbackForm from "./components/FeedbackForm.svelte";

import Feedbacklist from "./components/Feedbacklist.svelte";
import FeedbackStats from "./FeedbackStats.svelte";

	let feedback=[{
		id:1,
		rating:10,
		feedback:"Hey my name is nitish rana and i m goinf"
	},
	{
		id:2,
		rating:9,
		feedback:"thats the feedback 2 and i have to work"
	}];
	$:count = feedback.length
	$:average=feedback.reduce((prev,curr)=>prev+curr.rating,0)/count;

	const addFb=(e)=>{
		const newFeedback=e.detail;
		console.log(newFeedback)
		feedback=[newFeedback,...feedback];
	}
	const handleDelete =(e)=>{
		const itemID=e.detail;
		feedback=feedback.filter((item)=>item.id!=itemID)
	}
</script>

 
<main class="container">
 <FeedbackForm on:add-fb={addFb}/>
 <FeedbackStats {count} {average} />
 <Feedbacklist {feedback} on:delete-feedback={handleDelete}/>

</main>