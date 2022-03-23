<template>
	<div>
		<div id="carouselExampleDark" class="carousel carousel-dark slide" data-bs-ride="carousel">
		  <div class="carousel-indicators">
		    <button type="button" data-bs-target="#carouselExampleDark" data-bs-slide-to="0" class="active" aria-current="true" aria-label="Slide 1"></button>
		    <button type="button" data-bs-target="#carouselExampleDark" data-bs-slide-to="1" aria-label="Slide 2"></button>
		    <button type="button" data-bs-target="#carouselExampleDark" data-bs-slide-to="2" aria-label="Slide 3"></button>
		    <button type="button" data-bs-target="#carouselExampleDark" data-bs-slide-to="3" aria-label="Slide 4"></button>
		  </div>
		  <div class="carousel-inner">
		    <div class="carousel-item active" data-bs-interval="3000">
		      <img src="../static/first.png" class="d-block">
		      <div class="carousel-caption d-none d-md-block">
		        <h5>Gene Search</h5>
		        <p>Searches genes by name</p>
		      </div>
		    </div>
		    <div class="carousel-item" data-bs-interval="3000">
		      <img src="../static/second.png" class="d-block">
		      <div class="carousel-caption d-none d-md-block">
		        <h5>Gene Sequences</h5>
		        <p>Displays Gene sequences with graphical representations</p>
		      </div>
		    </div>
		    <div class="carousel-item" data-bs-interval="3000">
		      <img src="../static/third.png" class="d-block">
		      <div class="carousel-caption d-none d-md-block">
		        <h5>Protein Search</h5>
		        <p>Searches proteins by name</p>
		      </div>
		    </div>
		    <div class="carousel-item" data-bs-interval="3000">
		      <img src="../static/forth.png" class="d-block">
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

</script>

<style>
img{
	display: flex;
	justify-content: center;
	width: 100rem;
	height: 50rem;
	margin: 2rem;
}
</style>