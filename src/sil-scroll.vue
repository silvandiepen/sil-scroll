<script>
/* eslint-disable */
export default {
	bind: function(el, binding) {
		// Set the default settings
		let settings = {
			active: true,
			immidiate: true,
			element: window,
			fn: null
		};

		// Override settings
		if(!binding.value)
		if (binding.value.immidiate) settings.immidiate = binding.value.immidiate;
		if (binding.value.active) settings.immidiate = binding.value.active;
		if (binding.value.fn) settings.fn = binding.value.fn;
		if (binding.value.element == 'this') {
			settings.element = el;
		} else if (binding.value.element) {
			settings.element = binding.value.element;
		}

		const func = function(evt) {
			if (binding.value(evt, el)) {
				settings.element.removeEventListener('scroll', func);
				el.$destroy = () => settings.element.removeEventListener('scroll', func);
			} else if(setting.fn){
				settings.element.removeEventListener('scroll', settings.fn);
				el.$destroy = () => settings.element.removeEventListener('scroll',  settings.fn);			
			}
		};
		if (settings.immidiate) {
			func();
		}
		window.addEventListener('scroll', func);
	}
};
</script>
