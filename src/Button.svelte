<script>
    export let variant = 'success';
    export let inverse = false;
</script>


<button on:click class={variant} class:inverse={inverse}> <slot></slot></button>

<style>

    button{
        border-radius: 5px;
        padding: 8px;
        background-color: white;
        font-family: 'Roboto', sans-serif;
        margin: 8px 0px;
        width: auto;
        cursor: pointer;
    }

   .danger{
        border-color: #ff1605;
        align-self: flex-end;
        color: #ff1605
   }

   .danger:hover{
       box-shadow: 0px 0px 4px #ff1605 ;
   }

   .danger.inverse{
       background-color:#ff1605;
       color: white;
       align-self: flex-end;
   }

   .danger.inverse:hover{
    box-shadow: 0px 0px 4px #ff1605
   }


   .success{
        border-color: #059e00;
        color: #059e00;
   }

   .success:hover{
        box-shadow: 0px 0px 4px #059e00;
   }

   .success.inverse{
       background-color: #059e00;
       color: white;
   }

   .success.inverse:hover{
    box-shadow: 0px 0px 20px #059e00
   }

   .secondary{
       border-color: #f2028a;
       color: #f2028a;
   }

   .secondary:hover{
       box-shadow: 0px 0px 4px #f2028a;
   }
  
   .secondary.inverse{
       background-color: #f2028a;
       color: white;
   }

   .secondary.inverse:hover{
        box-shadow: 0px 0px 4px #f2028a
   }


</style>