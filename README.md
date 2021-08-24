Mirror the WordPress site:

```bash
wget -r -l inf --no-remove-listing --page-requisites --no-verbose -o debug.log http://innovationchallenge.open-contracting.org
```
- `-r -l inf --no-remove-listing` is the same as `--mirror`, without `--timestamping` to avoid `Last-modified header missing -- time-stamps turned off.` warnings.

Then, remove query strings from file names:

```bash
mv wp-includes/css/dist/block-library/style.min.css?ver=5.1.10 wp-includes/css/dist/block-library/style.min.css
mv wp-includes/js/wp-embed.min.js?ver=5.1.10 wp-includes/js/wp-embed.min.js
mv wp-content/themes/ocp/style.css?v=1.0 wp-content/themes/ocp/style.css
```

Some changes were made to WordPress:

- A hidden `div` with class `links` was removed from the theme, to not follow broken links.
- These lines were commented out in the `wp-includes/default-filters.php` file, to not download unnecessary files or follow broken links:

  - `add_action( 'xmlrpc_rsd_apis', 'rest_output_rsd' );`
  - `add_action( 'wp_head', 'feed_links', 2 );`
  - `add_action( 'wp_head', 'feed_links_extra', 3 );`
  - `add_action( 'wp_head', 'rsd_link' );`
  - `add_action( 'wp_head', 'wlwmanifest_link' );`
  - `add_action( 'wp_head', 'wp_shortlink_wp_head', 10, 0 );`
  - `add_action( 'wp_head', 'wp_oembed_add_discovery_links' );`

The `debug.log` file was then checked for `ERROR` messages.

A few manual changes were made:

- `http://` to `https://`
- Add missing images and assets
- Fix links to images and assets
