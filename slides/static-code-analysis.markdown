---
layout: slide
title:  Static Code Analysis
---

# Static Code Analysis

---

# Static Code Analysis

Static code analysis is a method of computer program debugging that is done by examining the code without executing the program. The process provides an understanding of the code structure, and can help to ensure that the code adheres to industry standards. Automated tools can assist programmers and developers in carrying out static analysis. The process of scrutinizing code by visual inspection alone (by looking at a printout, for example), without the assistance of automated tools, is sometimes called program understanding or program comprehension.

---

# Rubocop

A Ruby static code analyzer, based on the community Ruby style guide.

![](https://raw.githubusercontent.com/bbatsov/rubocop/master/logo/rubo-logo-horizontal.png)

RuboCop is a Ruby static code analyzer. Out of the box it will enforce many of the guidelines outlined in the community Ruby Style Guide.

Most aspects of its behavior can be tweaked via various configuration options.

Apart from reporting problems in your code, RuboCop can also automatically fix some of the problems for you.

--

## Installation

```bash
$ gem install rubocop
```

or using bundler

```ruby
gem 'rubocop', require: false
```

## Quickstart

```bash
$ cd my/cool/ruby/project
$ rubocop
```

--
## Report example

HTML Formatter

```bash
rubocop app -R --format html -o result.html
```

![](/assets/images/static_code_analysis/rubocop.png)

--
## Report example

JSON Formatter

```bash
rubocop app -R --format json -o result.json
```

```json
{
  "metadata": {
    "rubocop_version": "0.9.0",
    "ruby_engine": "ruby",
    "ruby_version": "2.0.0",
    "ruby_patchlevel": "195",
    "ruby_platform": "x86_64-darwin12.3.0"
  },
  "files": [{
      "path": "lib/foo.rb",
      "offenses": []
    }, {
      "path": "lib/bar.rb",
      "offenses": [{
          "severity": "convention",
          "message": "Line is too long. [81/80]",
          "cop_name": "LineLength",
          "corrected": true,
          "location": {
            "line": 546,
            "column": 80,
            "length": 4
          }
        }, {
          "severity": "warning",
          "message": "Unreachable code detected.",
          "cop_name": "UnreachableCode",
          "corrected": false,
          "location": {
            "line": 15,
            "column": 9,
            "length": 10
          }
        }
      ]
    }
  ],
  "summary": {
    "offense_count": 2,
    "target_file_count": 2,
    "inspected_file_count": 2
  }
}
```

--

### Awesome Rubocops docs here
http://rubocop.readthedocs.io/en/latest/

---

# Brakeman

A static analysis security vulnerability scanner for Ruby on Rails applications.

![](https://camo.githubusercontent.com/92cf013ec2d2c5538bd5d0ec8b1fd600d3614f2b/687474703a2f2f6272616b656d616e7363616e6e65722e6f72672f696d616765732f6c6f676f5f6d656469756d2e706e67)

Brakeman is an open source static analysis tool which checks Ruby on Rails applications for security vulnerabilities.

Check out Brakeman Pro if you are looking for a commercially-supported version with a GUI and advanced features.

--

# Installation

```bash
gem install brakeman
```

or using bundler:
```ruby
group :development do
  gem 'brakeman', :require => false
end
```

--

## Usage

```bash
brakeman
```

The output format is determined by the file extension or by using the -f option. Current options are: text, html, tabs, json, markdown, csv, and codeclimate

```bash
brakeman -o output.html -o output.json
```

--

## Report example

![](/assets/images/static_code_analysis/brakeman.png)


--

### Who is Using Brakeman?
* Code Climate
* GitHub
* Groupon
* New Relic
* Twitter

---

# Reek

Code smell detector for Ruby

![](https://github.com/troessner/reek/raw/master/logo/reek.text.png)


--

## Installation

```bash
gem install reek
```

## Run

```bash
reek [options] [dir_or_source_file]*
```


--

## Example

```ruby
# Smelly class
class Smelly
  # This will reek of UncommunicativeMethodName
  def x
    y = 10 # This will reek of UncommunicativeVariableName
  end
end
```

```bash
$ reek demo.rb
Inspecting 1 file(s):
S

demo.rb -- 2 warnings:
  [4]:UncommunicativeMethodName: Smelly#x has the name 'x' [https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Method-Name.md]
  [5]:UncommunicativeVariableName: Smelly#x has the variable name 'y' [https://github.com/troessner/reek/blob/master/docs/Uncommunicative-Variable-Name.md]
```

--

## Report example

```bash
reek app --format html > report.html
```

![](/assets/images/static_code_analysis/reek.png)

---

# SimpleCov

Code coverage for Ruby 1.9+ with a powerful configuration library and automatic merging of coverage across test suites

SimpleCov is a code coverage analysis tool for Ruby. It uses Ruby's built-in Coverage library to gather code coverage data, but makes processing its results much easier by providing a clean API to filter, group, merge, format, and display those results, giving you a complete code coverage suite that can be set up with just a couple lines of code.

--

## Getting started

1. Add SimpleCov to your `Gemfile` and `bundle install`:

    ```ruby
    gem 'simplecov', :require => false, :group => :test
    ```
2. Load and launch SimpleCov **at the very top** of your `test/test_helper.rb`
   (*or `spec_helper.rb`, cucumber `env.rb`, or whatever your preferred test
   framework uses*):

    ```ruby
    if ENV['RAILS_ENV'] == 'test'
      require 'simplecov'
      SimpleCov.start 'rails'
      puts "required simplecov"
    end
    ```

3. Run your tests, open up `coverage/index.html` in your browser and check out
   what you've missed so far.

4. Add the following to your `.gitignore` file to ensure that coverage results
   are not tracked by Git (optional):

    ```
    coverage
    ```

--

### Example output

**Coverage results report, fully browsable locally with sorting and much more:**

![SimpleCov coverage report](https://cloud.githubusercontent.com/assets/137793/17071162/db6f253e-502d-11e6-9d84-e40c3d75f333.png)

--

**Source file coverage details view:**

![SimpleCov source file detail view](https://cloud.githubusercontent.com/assets/137793/17071163/db6f9f0a-502d-11e6-816c-edb2c66fad8d.png)

---

### Overcommit

Overcommit is a gem for configuring Git hooks. It is excellent for keeping the code quality high. It allows tuning git hooks for linters launch before every commit.

* [Tutorial](https://medium.com/@kirill_shevch/lint-your-ruby-code-with-overcommit-and-static-analysis-tools-bd36d3147d2e)

---

### Code Analysis and Metrics Tools

* [Brakeman](https://github.com/presidentbeef/brakeman) - A static analysis security vulnerability scanner for Ruby on Rails applications.
* [Bullet](https://github.com/flyerhzm/bullet) - help you increase your application's performance by reducing the number of queries it makes
* [bundler-audit](https://github.com/rubysec/bundler-audit) - Patch-level verification for bundler.
* [Fasterer](https://github.com/DamirSvrtan/fasterer) - Make your Rubies go faster with this command line tool highly inspired by fast-ruby and Sferik's talk at Baruco Conf.
* [Reek](https://github.com/troessner/reek) - Code smell detector for Ruby.
* [RuboCop](https://github.com/bbatsov/rubocop) - A static code analyzer, based on the community Ruby style guide.
* [Pry](https://github.com/pry/pry) - A runtime developer console and IRB alternative with powerful introspection capabilities.
* [SimpleCov](https://github.com/colszowka/simplecov) - Code coverage for Ruby 1.9+ with a powerful configuration library and automatic merging of coverage across test suites.
* [Traceroute](https://github.com/amatsuda/traceroute) - A Rake task gem that helps you find the dead routes and actions for your Rails 3+ app
* [Active Record Doctor](https://github.com/gregnavis/active_record_doctor) - Identify database issues before they hit production.
* [Overcommit](https://github.com/sds/overcommit) - A fully configurable and extendable Git hook manager.
* [lol_dba](https://github.com/plentz/lol_dba) - A small package of rake tasks that scan your application models and displays a list of columns that probably should be indexed. Also, it can generate .sql migration scripts.
---

# Control questions

- What is `Rubocop`?
- What is `Fasterer`?
- What is `Simplecov`?
- What is `Overcommit`?
- Why is it important to follow ruby style guide?

---

# The End
