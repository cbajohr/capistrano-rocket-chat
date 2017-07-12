# capistrano-rocket-chat
rocket.chat webhook gem for [Capistrano 3](https://github.com/capistrano/capistrano). 

## Installation

Add this line to your application's *Gemfile*:

```ruby
gem 'capistrano-rocket-chat'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install capistrano-rocket-chat

In your *Capfile* add this line:

```ruby
require 'capistrano/rocket_chat'
```

Add the rocket.chat webhook url including the webhook token to your *deploy.rb* file:

```ruby
set :rocket_chat_webhook_url, "https://mychat.com/hooks/MYTOKEN"
```


_Optionnal_

If you want override the channel directly in the capistrano config:

```
set :rocket_chat_channel, "#CHANNEL"
```

And you are ready to go

## Usage

The webhook fires automatically on the following capistrano events: 
* deploy:starting
* deploy:failed
* deploy:finished

Additionally you will need a parser script for your rocket.chat for the incoming webhook integration.

If you don't want to code one yourself, here is a working script with basic functionality for you:
https://github.com/cbajohr/capistrano-rocket-chat/wiki/rocket.chat-parser-script-example


## Post examples

Example JSON that is pushed by the gem.

Possible 'event -> hook' states are:
* starting
* failed
* finished

```JSON
{
  "event": {
    "hook": "failed",
    "text": "failed deployment to 'www.server.de' on branch 'master' to stage 'production'"
  },
  "attributes": {
    "rocket_chat_url": "http://mychat.com/mytoken",
    "rocket_chat_channel": "#test",
    "application": "my_application",
    "branch": "master",
    "repo_url": "git@my_git.com/repo/repo",
    "stage": "production",
    "deploy_to": "/var/www/my_vhost_name",
    "rails_env": "production",
    "scm": "git",
    "log_level": "debug",
    "local_user": "johndoe",
    "server": {
      "name": "my_server.com",
      "user": "my_ssh_user"
    }
  }
}
```

The rocketchat channel is passed in the JSON if only you have defined it in the capistrano config.

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `rake test` to run the tests. You can also run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release`, which will create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/cbajohr/capistrano-rocket-chat. This project is intended to be a safe, welcoming space for collaboration, and contributors are expected to adhere to the [Contributor Covenant](http://contributor-covenant.org) code of conduct.

## License

The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).

