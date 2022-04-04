<template>
	<div>
		<div id="carouselExampleDark" class="carousel carousel-dark slide" data-bs-ride="carousel">
		  <div class="carousel-inner">
		    <div class="carousel-item active" data-bs-interval="3000">
		      <img src="../static/first.png" class="img-fluid">
		      <div class="carousel-caption d-none d-md-block">
		        <h5>Gene Search</h5>
		        <p>Searches genes by name</p>
		      </div>
		    </div>
		    <div class="carousel-item" data-bs-interval="3000">
		      <img src="../static/second.png" class="img-fluid">
		      <div class="carousel-caption d-none d-md-block">
		        <h5>Gene Sequences</h5>
		        <p>Displays Gene sequences with graphical representations</p>
		      </div>
		    </div>
		    <div class="carousel-item" data-bs-interval="3000">
		      <img src="../static/third.png" class="img-fluid">
		      <div class="carousel-caption d-none d-md-block">
		        <h5>Protein Search</h5>
		        <p>Searches proteins by name</p>
		      </div>
		    </div>
		    <div class="carousel-item" data-bs-interval="3000">
		      <img src="../static/forth.png" class="img-fluid">
		      <div class="carousel-caption d-none d-md-block">
		        <h5>Protein Sequences</h5>
		        <p>Displays Protein sequences with graphical representations</p>
		      </div>
		    </div>
		  </div>
		</div>
	</div>
</template>

<script>
export default{
head(){
    return{
      title: "New Genomi",
      meta:[
        {
          hid: "description",
          name: "viewpoint",
          content: "width=device-width, initial-scale=1"
        }
      ]
    };
  }
}
</script>

<style>
img{
	display: flex;
	justify-content: center;
	width: 87rem;
	height: 40rem;
	margin: 1rem;
}
@media only screen and (max-width: 480px) {
  img {
    margin: 0rem;
  }
}
</style>