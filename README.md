Hesperides
==========

Hesperides is a platform that enables people to crowdfund incredibly ambitious goals.

Each goal on the platform has an associated multi-signature bitcoin wallet, the signatures to which are distributed to some number of experts who hold the authority to deem the goal achieved. Anybody can transfer bitcoin to the wallet, but in order to unlock the wallet to disburse the funds, a supermajority of experts need to agree to that decision.

Some ideas for potential goals:

- Space exploration
- Cures for orphan diseases
- Vaccines



##Tech Stack

### Requirements

To run the specs or fire up the server, be sure you have these installed:

* Ruby 2.1 (see [.ruby-version](.ruby-version)).
* PostgreSQL 9.x (```brew install postgresql```) with superuser 'postgres' with no password (```createuser -s postgres```).
* PhantomJS for Capybara and Javascript testing (```brew install phantomjs```).

### First Time Setup

After cloning, run these commands to install missing gems and prepare the database.

    $ gem install bundler
    $ bundle
    $ rake db:setup db:sample_data

Note, ```rake db:sample_data``` loads a small set of data for development. Check out [db/sample_data.rb](db/sample_data.rb)
for details.

### Running the Specs

To run all Ruby and Javascript specs.

    $ rake

### Running the Application Locally

    $ foreman start
    $ open http://localhost:3000


## Additional Development Details

### Code Coverage (local)

Coverage for the ruby specs:

    $ COVERAGE=true rspec

Code coverage is reported to Code Climate on every CI build so there's a record of trending.

### Using Guard

Guard is configured to run ruby and jasmine specs, and also listen for livereload connections.

    $ bundle exec guard

### Using Mailcatcher

    $ gem install mailcatcher
    $ mailcatcher
    $ open http://localhost:1080/

Learn more at [mailcatcher.me](http://mailcatcher.me/). And please don't add mailcatcher to the Gemfile.

### Continuous Integration and Deployment with CircleCI

This project is configured for continuous integration and deployment with CircleCI and Heroku.

Check out [circle.yml](circle.yml) and [bin/deploy.sh](bin/deploy.sh) for details.

# Server Environments

### Environment Variables

Several common features and operational parameters can be set using environment variables.

**Required**

* ```SECRET_KEY_BASE``` - Secret key base for verfying signed cookies. Should be 30+ random characters and secret!

**Optional**

* ```HOSTNAME``` - Canonical hostname for this application. Other incoming requests will be redirected to this hostname.
* ```BASIC_AUTH_PASSWORD``` - Enable basic auth with this password.
* ```BASIC_AUTH_USER``` - Set a basic auth username (not required, password enables basic auth).
* ```PORT``` - Port to listen on (default: 3000).
* ```UNICORN_WORKERS``` - Number of unicorn workers to spawn (default: development 1, otherwise 3).
* ```UNICORN_BACKLOG``` - Depth of unicorn backlog (default: 16).

