# Google Dorking

[Search Engine Optimisation (SEO) checkup tool](https://web.dev/measure/) <--

| Term      | Action                                                       |
| --------- | ------------------------------------------------------------ |
| site:     | returns results only from the specified website address      |
| inurl:    | returns results that have the specified word in the URL      |
| intitle:  | returns results that contain the specified word in the title |
| filetype: | returns results which are a particular file extension        |
| cache:    | View Google's Cached version of a specified URL              |

## Robots.txt

- Allowing direcroties:

    ```yaml
    User-agent: *
    Allow: /

    Sitemap: http://mywebsite.com/sitemap.xml
    ```
- Disallowing directories:

    ```yaml
    User-agent: *
    Disallow: /super-secret-directory/
    Disallow: /not-a-secret/but-this-is/

    Sitemap: http://mywebsite.com/sitemap.xml
    ```
- Allowing crawlers:

    ```yaml
    User-agent: Googlebot
    Allow: /

    User-agent: msnbot
    Disallow: /
    ```

- Disallowing files: (We can use [regexing](https://www.rexegg.com/regex-quickstart.html))

    ```yaml
    User-agent: *
    Disallow: /*.ini$
    ```

## Sitemap.xml

- Simple example of sitemap.xml:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
     <url>
      <loc>https://seosherpa.com/</loc>
      <lastmod>2022-01-26T19:12:36+09:00</lastmod>
            <changefreq>Daily</changefreq>
            <priority>1</priority>
     </url>
     <url>
      <loc>https://seosherpa.com/services/</loc>
      <lastmod>2021-11-16T13:21:20+09:00</lastmod>
            <changefreq>Daily</changefreq>
            <priority>0.8</priority>
     </url>
    </urlset>
    ```