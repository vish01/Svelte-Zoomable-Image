<script>
	export let x = 0,
		y = 0,
		normalImage = 'https://via.placeholder.com/670x380.png/0000FF?text=This+is+A+Test',
		zoomedImage = 'https://via.placeholder.com/1340x760.png/0000FF?text=This+is+A+Test',
		currentImage = normalImage;

	function setZoom(clientX, clientY, image) {
		x = clientX;
		y = clientY;
		currentImage = image;
	}

	function handleZoomEvent(e) {
		switch (e.type) {
			case 'mousemove':
				setZoom(-e.offsetX, -e.offsetY, zoomedImage);
				break;
			case 'mouseleave':
				setZoom(0, 0, normalImage);
				break;
			case 'mousedown':
				setZoom(-e.offsetX, -e.offsetY, zoomedImage);
				break;
			case 'mouseup':
				setZoom(0, 0, normalImage);
				break;
			case 'touchmove':
				setZoom(-e.touches[0].clientX, -e.touches[0].clientY, zoomedImage);
				break;
			case 'touchstart':
				setZoom(-e.touches[0].clientX, -e.touches[0].clientY, zoomedImage);
				break;
			case 'touchend':
				setZoom(0, 0, normalImage);
				break;
		}
	}
</script>

<div
	class="zoom-handler"
	on:mousedown={handleZoomEvent}
	on:mouseup={handleZoomEvent}
	on:mousemove={handleZoomEvent}
	on:mouseleave={handleZoomEvent}
	on:touchstart={handleZoomEvent}
	on:touchmove={handleZoomEvent}
	on:touchend={handleZoomEvent}
	style="background-image: url({currentImage}); background-position-x:{x}px; background-position-y:{y}px;" />

<style>
	.zoom-handler {
		overflow: auto;
		width: 677px;
		max-width: 100%;
		height: 347px;
		cursor: crosshair;
		background-repeat: no-repeat;
		touch-action: none;
	}
</style>
