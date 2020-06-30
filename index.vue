<!-- ///

Brand Pattern

Makes it easy to reuse and manipulate SVGs. For example:

<brand-pattern
  :type="diagonal--bottomright"
  :color="green"
></brand-pattern>

/// -->

<template>
  <svg aria-hidden="true" viewBox="0 0 100 100"
    :class="options.class"
    :preserveAspectRatio="options.preserveAspectRatio"
  >
    <g :transform="options.transform">
      <template v-if="options.template === 'gradient--focus'">
        <rect x="0" width="100" height="100" />
        <rect x="20" width="77" height="100" />
        <rect x="35" width="59.5" height="100" />
        <rect x="50" width="42" height="100" />
        <rect x="65" width="24.2" height="100" />
      </template>

      <template v-if="options.template === 'circles'">
        <g transform="scale(1.42)">
          <circle r="100" />
          <circle r="83.3" />
          <circle r="66.7" />
          <circle r="50" />
          <circle r="33.3" />
          <circle r="16.7" />
        </g>
      </template>

      <template v-if="options.template === 'columns'">
        <rect x="0" width="100" height="200" />
        <rect x="20" width="80" height="200" />
        <rect x="40" width="60" height="200" />
        <rect x="60" width="40" height="200" />
        <rect x="80" width="20" height="200" />
      </template>

      <template v-if="options.template === 'rays'">
        <rect width="1000" height="100" />
        <rect width="1000" height="100" transform="rotate(26.6)" />
        <rect width="1000" height="100" transform="rotate(40)" />
        <rect width="1000" height="100" transform="rotate(53)" />
        <rect width="1000" height="100" transform="rotate(65)" />
        <rect width="1000" height="100" transform="rotate(73.7)" />
      </template>

      <template v-if="options.template === 'squares'">
        <rect x="-100" y="-100" width="200" height="200" />
        <rect x="-75" y="-75" width="150" height="150" rx="3.5" />
        <rect x="-50" y="-50" width="100" height="100" rx="3.5" />
        <rect x="-25" y="-25" width="50" height="50" rx="3.5" />
      </template>
    </g>
  </svg>
  <!-- eslint-enable -->
</template>

<script>
  // Once IE11 is dropped, we can just use the variables in `_vars.css`
  const colorMap = {
    blue: {
      '50': '#e8f0fe',
      '100': '#d2e3fc',
      '200': '#aecbfa',
      '300': '#8ab4f8',
      '400': '#669df6',
      '500': '#4285f4',
      '600': '#1a73e8',
      '700': '#1967d2',
      '800': '#185abc',
      '900': '#174ea6',
    },

    green: {
      '50': '#e6f4ea',
      '100': '#ceead6',
      '200': '#a8dab5',
      '300': '#81c995',
      '400': '#5bb974',
      '500': '#34a853',
      '600': '#1e8e3e',
      '700': '#188038',
      '800': '#137333',
      '900': '#0d652d',
    },

    grey: {
      '50': '#f8f9fa',
      '100': '#f1f3f4',
      '200': '#e8eaed',
      '300': '#dadce0',
      '400': '#bdc1c6',
      '500': '#9aa0a6',
      '600': '#80868b',
      '700': '#5f6368',
      '800': '#3c4043',
      '900': '#202124',
    },

    orange: {
      '50': '#fedfc8',
      '100': '#fdc69c',
      '200': '#fcad70',
      '300': '#fa903e',
      '400': '#fa7c16',
      '500': '#fa7c16', // Same as 400
    },

    pink: {
      '50': '#fecfe8',
      '100': '#fba9d6',
      '200': '#ff8bcc',
      '300': '#ff63b8',
      '400': '#f43aa1',
      '500': '#e52592',
    },

    purple: {
      '50': '#e9d3fd',
      '100': '#d8aefb',
      '200': '#c58afa',
      '300': '#af5cf7',
      '400': '#a143f5',
      '500': '#a143f5', // Same as 400
    },

    red: {
      '50': '#fce8e6',
      '100': '#fad2cf',
      '200': '#f6aea9',
      '300': '#f28b82',
      '400': '#ee675c',
      '500': '#ea4335',
      '600': '#d93025',
      '700': '#c5221f',
      '800': '#b31412',
      '900': '#a50e0e',
    },

    // TODO: Rename 'teal' to 'cyan' everywhere
    teal: {
      '50': '#ccf0f8',
      '100': '#a1e5f2',
      '200': '#78d9ed',
      '300': '#4ecde6',
      '400': '#25c1e0',
      '500': '#25c1e0', // Same as 400
    },

    yellow: {
      '50': '#fef7e0',
      '100': '#feefc3',
      '200': '#fde293',
      '300': '#fdd663',
      '400': '#fcc934',
      '500': '#fbbc04',
      '600': '#f9ab00',
      '700': '#f29900',
      '800': '#ea8600',
      '900': '#e37400',
    },
  };

  const presetTypes = {
    'bar--left': {
      class: 'bar',
      objectFit: 'none',
      template: 'gradient--focus',
      transform: 'rotate(180, 50, 50)',
    },
    'bar--left--choppy': {
      class: 'bar',
      intensities: ['100', '50', '200', '400', '200'],
      objectFit: 'none',
      template: 'gradient--focus',
      transform: 'rotate(180, 50, 50)',
    },
    'bar--right': {
      aspect: 'none',
      class: 'bar',
      objectFit: 'none',
      template: 'gradient--focus',
    },
    'bar--bottom': {
      class: 'bar--v',
      intensities: ['50', '100', '200', '300', '500'],
      objectFit: 'none',
      template: 'gradient--focus',
      transform: 'rotate(90, 50, 50)',
    },
    'diagonal--bottomright': {
      intensities: ['50', '100', '200', '300', '500'],
      objectFit: 'cover',
      origin: 'bottomright',
      template: 'columns',
      transform: 'scale(1.56) rotate(45, 100, 100) translate(-50, 0)',
    },
    'diagonal--topright': {
      intensities: ['50', '100', '200', '300', '400'],
      objectFit: 'cover',
      origin: 'topright',
      template: 'columns',
      transform: 'scale(1.56) rotate(-45, 100, 0) translate(-22, -100)',
    },
    'radiate--bottomright': {
      objectFit: 'cover',
      origin: 'bottomright',
      template: 'circles',
      transform: 'translate(-30, -30) scale(1.3) rotate(180, 50, 50)',
    },
    'radiate--middleright': {
      objectFit: 'cover',
      origin: 'middleright',
      template: 'circles',
      transform: 'translate(0, -50) translate(-5, -5) scale(1.05) rotate(180, 50, 50)',
    },
    'rays--bottomleft': {
      objectFit: 'cover',
      origin: 'bottomleft',
      template: 'rays',
      transform: 'rotate(-90, 50, 50)',
    },
    'rays--bottommiddle': {
      objectFit: 'cover',
      origin: 'bottommiddle',
      template: 'rays',
      transform: 'translate(-20, 0) rotate(-90, 50, 50)',
    },
    'squares--bottomleft': {
      objectFit: 'cover',
      origin: 'bottomleft',
      template: 'squares',
      transform: 'rotate(-90, 50, 50)',
    },
    'strip--left': {
      class: 'strip',
      intensities: ['400', '300', '200', '100', '50'],
      template: 'columns',
    },
    'strip--right': {
      class: 'strip',
      intensities: ['50', '100', '200', '300', '400'],
      template: 'columns',
    },
  };

  const originMap = {
    'topleft': 'xMinYMin',
    'topmiddle': 'xMidYMin',
    'topright': 'xMaxYMin',
    'middleleft': 'xMinYMid',
    'middle': 'xMidYMid',
    'middleright': 'xMaxYMid',
    'bottomleft': 'xMinYMax',
    'bottommiddle': 'xMidYMax',
    'bottomright': 'xMaxYMax',
  };

  const objectFitMap = {
    'cover': 'slice',
    'contain': 'meet',
    'none': 'none',
  };

  const props = {
    color: {
      template: (String || Array),
      required: false,
      default: '',
    },
    intensities: {
      template: (Array || undefined),
      required: false,
      default: undefined,
    },
    objectFit: {
      template: String,
      required: false,
      default: '',
    },
    origin: {
      template: String,
      required: false,
      default: '',
    },
    transform: {
      template: String,
      required: false,
      default: '',
    },
    type: {
      template: String,
      required: false,
      default: '',
    },
  };

  const defaults = () => ({
    color: 'blue',
    intensities: ['50', '100', '200', '300', '400', '500', '600', '700', '800', '900'],
    objectFit: 'cover',
    origin: 'topleft',
    template: 'circles',
  });

  export default {
    name: 'brand-svg',
    props,

    computed: {
      options() {
        const options = {};
        const type = this.type;
        const presetType = presetTypes[type];
        Object.assign(options, {
          ...defaults(),
          ...(presetType || {}),
        });

        for (const key in props) {
          if (this[key]) {
            options[key] = this[key];
          }
        }

        if (options.objectFit === 'none') {
          options.preserveAspectRatio = 'none';
        } else {
          options.preserveAspectRatio = `${originMap[options.origin]} ${objectFitMap[options.objectFit]}`;
        }

        if (options.color instanceof Array) {
          options.colors = [...options.color];
        } else {
          options.colors = options.intensities.map(intensity => colorMap[options.color][intensity]);
        }
        return options;
      },
    },

    mounted() {
      try {
        const elements = [...this.$el.querySelectorAll('rect, circle')];
        if (elements.length === 0) {
          console.log(`SVG not generated: No template for '${this.options.template}'.`);
          throw new Error();
        }
        for (const index in elements) {
          const el = elements[index];
          el.setAttribute('fill', this.options.colors[index]);
        }
      } catch (e) {
        console.log(`SVG not generated: '${this.options.type}' in '${this.options.color}'.`);
      }
    },
  };
</script>

<style lang="postcss" scoped>
svg {
  display: block;
  height: 100%;
  width: 100%;
}

.bar {
  height: 18px;
}

.bar--v {
  width: 18px;
}

.strip {
  height: 4px;
}
</style>
