### goliath
---
https://github.com/postrank-labs/goliath

```
gem install rvm
rvm install 1.9.3
rvm use 1.9.3
gem install goliath

ruby hello.rb -sv
```

```ruby
require 'goliath'
class Hello < Goliath::API
  def response(env)
    [200, {}, "Hello"]
  end
end

require 'goliath'
require 'em-synchrony'
require 'em-synchrony/em-http'
class HelloWorld < Goliath::API
  def response(env)
    req = EM::HttpRequest.new("http://www.google.com/").get
    resp = req.response
    [200, {}, resp]
  end
end

# config/echo.rb
require 'mysql2/em_fiber'
config['db'] = EM::Synchrony::ConnectionPool.new(:size => 20) do
    ::Mysql2::EM::Fiber::Client.new(:host => 'localhost', :username => 'test',
                                    :password => 'password', :socket => nil,
                                    :database => 'echo_db',
                                    :resconnect => true)
end

# echo.rb
require 'goliath'
class Echo < Goliath::API
  def response(env)
    ret = db.query("SELECT sleep(1)")
    [200, {}, ret]
  end
end

```

```
```


