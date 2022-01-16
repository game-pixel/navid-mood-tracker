<script>
    import supabase from '$lib/db';

    let emojiList = {
   	 worst: '😭',
   	 bad: '🙁',
   	 okay: '😐',
   	 good: '🙂',
   	 best: '😁'
    };

    let emoji = '😐';

    let day = '1';
    let month = '1';
    let year = '2021';
    let mood = 'Okay';
    let comment = 'This is a comment';

    // Insert entry
    async function saveEntry() {
   	 const { error } = await supabase.from('moodEntries').insert(
   		 {
   			 user_id: supabase.auth.user().id,
   			 day: day,
   			 month: month,
   			 year: year,
   			 mood: mood,
   			 comment: comment
   		 }
   	 );
   	 if (error) alert(error.message);

   	 location.reload(); // Refresh the page.
    }
</script>

<div class="modal fade" id="newEntry" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
   	 <div class="modal-content">
   		 <div class="modal-header">
   			 <h5 class="modal-title">New Entry</h5>
   			 <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close" />
   		 </div>
   		 <div class="modal-body">
   			 <!-- Date Input -->
   			 <div class="row">
   				 <div class="col">
   					 <form class="form-floating">
   						 <input
   							 type="number"
   							 class="form-control"
   							 id="dayInput"
   							 bind:value={day}
   							 min="1"
   							 max="31"
   						 />
   						 <label for="dayInput">Day</label>
   					 </form>
   				 </div>