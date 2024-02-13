---
layout: post
title:  "Github blog 업로드 오류"
excerpt: "Github blog 업로드 오류"

tags:
  - [Blog, jekyll, Github, Error]

toc: true
toc_sticky: true

date: 2024-02-13
last_modified_at: 2024-02-13
---

{% include toc.html %}

### Error 발생
오늘 강의 정리를 끝내고 블로그에 업로드했는데 오류가 발생했다.     

```python
Error:  Logging at level: debug Configuration file: /github/workspace/./_config.yml GitHub Pages: github-pages v229 GitHub Pages: jekyll v3.9.4 Theme: jekyll-theme-primer Theme source: /usr/local/bundle/gems/jekyll-theme-primer-0.6.0 Requiring: jekyll-github-metadata Requiring: jekyll-seo-tag Requiring: jekyll-mentions Requiring: jekyll-feed Requiring: jekyll-sitemap Requiring: jekyll-gist Requiring: jekyll-paginate Requiring: jekyll-coffeescript Requiring: jekyll-commonmark-ghpages Requiring: jekyll-github-metadata Requiring: jekyll-relative-links Requiring: jekyll-optional-front-matter Requiring: jekyll-readme-index Requiring: jekyll-default-layout Requiring: jekyll-titles-from-headings GitHub Metadata: Initializing... Source: /github/workspace/./ Destination: /github/workspace/./_site Incremental build: disabled. Enable with --incremental Generating... EntryFilter: excluded /LICENSE EntryFilter: excluded /Gemfile EntryFilter: excluded /README.md EntryFilter: excluded /Gemfile.lock Reading: _posts/2022-12-01-pytorch.md Reading: _posts/2023-08-28-linearalgebra1.md Reading: _posts/2023-06-25-deeplearning1.md Reading: _posts/2024-02-02-IT용어.md Reading: _posts/2013-05-22-sample-post-images.md Reading: _posts/2024-02-01-chunjae4.md Reading: _posts/2016-03-21-ramme-theme.md Reading: _posts/2013-08-16-code-highlighting-post.md Reading: _posts/2024-01-29-chunjae3.md Reading: _posts/2024-02-06-chunjae6.md Reading: _posts/2023-03-09-linux.md Reading: _posts/2023-04-20-mysql_4.md Reading: _posts/2023-03-23-linux_3.md Reading: _posts/2023-04-19-mysql _3.md Reading: _posts/2023-05-03-pytorch4.md Reading: _posts/2024-01-29-chunjae1.md Reading: _posts/2024-02-13-chunjae8.md Reading: _posts/2023-04-27-git1.md Reading: _posts/2023-05-02-pytorch3.md Reading: _posts/2023-04-21-seederror.md Reading: _posts/2024-02-07-chunjae7.md Reading: _posts/2022-11-30-mogak.md Reading: _posts/2023-05-02-pytorch2.md Reading: _posts/2024-02-05-IT용어2.md Reading: _posts/2023-04-19-mysql.md Reading: _posts/2023-04-21-mysql_5.md Reading: _posts/2022-11-30-testpost.md Reading: _posts/2023-02-07-python.md Reading: _posts/2023-01-19-error.md Reading: _posts/2023-04-19-mysql _2.md Reading: _posts/2024-02-05-chunjae5.md Reading: _posts/2024-01-29-chunjae2.md Reading: _posts/2023-03-14-linux_2.md Reading: _posts/2023-05-01-pytorch1.md Reading: _posts/2023-03-09-linux_1.md Reading: _posts/2023-08-22-PS1.md Reading: _posts/2023-10-05-mysql6.md Generating: JekyllOptionalFrontMatter::Generator finished in 3.0998e-05 seconds. Generating: JekyllReadmeIndex::Generator finished in 5.5884e-05 seconds. Jekyll Feed: Generating feed for posts Generating: JekyllFeed::Generator finished in 0.000656412 seconds. Generating: Jekyll::JekyllSitemap finished in 0.001579348 seconds. Generating: Jekyll::Paginate::Pagination finished in 4.217e-06 seconds. github-pages 229 | Error: undefined method `excerpt_separator' for #<Jekyll::Page @name="index.md"> 
```

오류로 github-pages v229로 업데이트하면서 의존성 문제가 발생해서 빌드가 안되는 것이다.     
상당히 최근에 업데이트가 되어서 자료도 별로없었고, 찾아도 처리가 안되는 경우가 많았다.    
따라서 많은 검색 결과     

```python
.github/workflow
```    

폴더에 있는 jekyll-gh-pages.yml 파일에서    

```python
        uses: actions/jekyll-build-pages@v1.0.9
```
로 빌드 버전을 설정해줘서 해결했다.     

이후에 정상적으로 업로드가 된다.     


블로그를 연지 일년이 지났는데 갑자기 발생한 오류라서 당황스러웠지만 역시 차근차근 검색을 하는 것이 중요하다는 것을 다시 한번 깨닫고 간다.....