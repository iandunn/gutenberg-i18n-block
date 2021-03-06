# Gutenberg I18N Block

This is a proof-of-concept to demonstrate how a fully internationalised an localised Gutenberg block works.

**Note:** These internationalisation tools used in this sample plugin are still under development. Things will eventually change and get less complex.

## Usage

If you want to apply the I18N functionality from this block to yours, you need three main scripts:

1. `npm run build`  
This command runs [Babel](https://babeljs.io/) to transpile our modern JavaScript from `block/src/block.js` to something more browsers understand in `block/block.js`. It uses the [@wordpress/babel-plugin-makepot](https://www.npmjs.com/package/@wordpress/babel-plugin-makepot) Babel plugin to automatically extract all translatable strings from the JavaScript and create a POT file for them (`gutenberg-i18n-block-js.pot`).
2. `npm run pot-to-php`  
Takes the POT file from the previous step and generates a fake PHP file containing these translatable strings.
3. `npm run makepot`  
Since now all translatable texts are in PHP, we can use the  [`wp i18n make-pot`](https://github.com/wp-cli/i18n-command) command to create our final POT file that contains all texts from both the PHP side as well as the JavaScript side (`gutenberg-i18n-block.pot`). It also allows us to translate the plugin's name and description.

### Advanced

If you want to load the JavaScript translations separately, you could create a new PO/MO file based on `gutenberg-i18n-block-js.pot` and then load these via `load_plugin_textdomain()` just when needed. To make things easier, you could use a separate text domain for that.

This really only gets interesting for larger projects where you have many strings to translate in both PHP and JS. Keeping these separated means you don't unnecessarily load multiple KB of translations when you don't need them (e.g. when you're not in the Gutenberg editor).

## Screenshots

![Editor in English](https://cldup.com/vGpWmoUARj.png)

![Block in English](https://cldup.com/Fd66YdpuPw.png)

![Editor in German](https://cldup.com/8hf2Sihuew.png)

![Block in German](https://cldup.com/O2jrOcXu-K.png)
