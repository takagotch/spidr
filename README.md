### spidr
---
https://github.com/postmodern/spidr

```ruby
Spidr.start_at('http://tenderlovemaking.com/')
Spidr.host('solnic.eu')
Spidr.site('http://www.rubyflow.com/')

Spidr.start_at(
  'http://company.com/',
  hosts: [
    'company.com',
    /host[\d]+\.company\.com/
  ]
)

Spdir.site('http://company.com/', ignore_links: [%(^/blog/)])
Spdir.site('http://company.com/', ignore_ports: [8000, 8010, 8080])

Spidr.site(
  'http://company.com/',
  robots: true
)

Spidr.site('http://www.rubyinside.com/') do |spider|
  spider.every_url { |url| puts url }
end

url_map = Hash.new { |hash, key| hash[key] = [] }
Spidr.site('http://intracet.com/') do |spider|
  spider.every_link do |origin,dest|
    url_map[dest] << origin
  end
end

Spidr.site('http://company.com/') do |spider|
  spider.every_failed_url { |url| puts url }
end

url_map = Hash.new { |hash, key| hash[key] = [] }
spider = Spidr.site('http://intranet.com/') do |spider|
  spider.every_link do |origin,dest|
    url_map[dest] << origin
  end
end
spider.failures.each do |url|
  puts "Broken link #{url} found in:"
  url_map[url].each { |page| puts " #{page}" }
end

Spidr.site('http://comapy.com/') do |spider|
  spider.every_page do |page|
    puts ">>> #{page.url}"
    page.search('//meta').each do |meta|
      name = (meta.attributes['name'] || meta.attributes['http-equiv'])
      value = meta.attributes['content']
      puts " #{name} = #{value}"
    end
  end
end

Spidr.site('http://www.ruby-lang.org/') do |spider|
  spider.every_html_page do |page|
    puts page.title
  end
end

servers = Set[]
Spidr.host('company.com') do |spider|
  spider.all_headers do |headers|
    servers << headers['server']
  end
end

Spidr.host('company.com') do |spider|
  spider.every_forbidden_page do |page|
    spider.pause!
  end
end

Spidr.host('company.com') do |spider|
  spider.every_missing_page do |page|
    spider.skip_page!
  end
end

Spidr.host('company.com') do |spider|
  spider.every_url do |url|
    if url.path.split('/').find { |dir| dir.to_i > 1000 }
      spider.skip_link!
    end
  end
end
```

```
gem install spidr
```

```
```

