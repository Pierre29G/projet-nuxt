<template>

<form id="formspree-form"
  action="https://formspree.io/f/xzbogldg"
  method="POST"
  >
  <Input type="email" name="email"/>
  <Input type="message" name="message"/>

  
  <!-- your other form fields go here -->
  <button type="submit">Send</button>
  <p id="my-form-status"></p>
</form>

</template>

<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>

<script>
  export default {
data () {
    return {
      info: null,
      loading: true,
      errored: false
    }
  },
  mounted () {
    var form = document.getElementById("formspree-form");
    
    async function handleSubmit(event) {
      event.preventDefault();
      var status = document.getElementById("my-form-status");
      var data = new FormData(event.target);
      fetch(event.target.action, {
        method: form.method,
        body: data,
        headers: {
            'Accept': 'application/json'
        }
      }).then(response => {
        if (response.ok) {
          status.innerHTML = "Message envoyé !";
          form.reset()
        } else {
          response.json().then(data => {
            if (Object.hasOwn(data, 'errors')) {
              status.innerHTML = data["errors"].map(error => error["message"]).join(", ")
            } else {
              status.innerHTML = "Oops! There was a problem submitting your form"
            }
          })
        }
      }).catch(error => {
        status.innerHTML = "Oops! There was a problem submitting your form"
      });
    }
    form.addEventListener("submit", handleSubmit)
  }
  }
</script>