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
		  <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleDark" data-bs-slide="prev">
		    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
		    <span class="visually-hidden">Previous</span>
		  </button>
		  <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleDark" data-bs-slide="next">
		    <span class="carousel-control-next-icon" aria-hidden="true"></span>
		    <span class="visually-hidden">Next</span>
		  </button>
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
    width: auto;
    margin: 0rem;
    height: auto;
  }
}
</style>