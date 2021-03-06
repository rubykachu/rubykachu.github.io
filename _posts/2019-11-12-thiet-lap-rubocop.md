---
layout: post
title: "Hướng dẫn bắt lỗi convention trong Rails"
date: 2019-11-12 10:54:00 +0700
categories: Rails
tags: rubocop reek lint rails
author: minhtang
description: "Hướng dẫn bắt lỗi convention trong Rails, giúp code tối ưu và tiết kiệm thời gian khi review"
permalink: /thiet-la-rubocop-trong-rails
---

* content
{:toc}
Rubocop, reek, slim-lint là một công cụ để kiểm tra code style được xây dựng phục vụ cho developers.

Rubocop sử dụng các quy tắc được định sẵn để so sánh chúng với code của bạn rồi đưa ra các thông báo lỗi.

Sử dụng Rubocop trong projects giúp chúng ta tiết kiệm thời gian cho việc review coding convention và đảm bảo code không mắc phải những lỗi convention cơ bản.




## Cài đặt

Trong Gemfile:

```ruby
group :development, :test do
  # Lint
  gem 'rubocop'
  gem 'rubocop-performance'
  gem 'rubocop-rails'
  gem 'reek'
  gem 'slim'
end

group :development do
  # Lint
  gem 'slim_lint'
end
```

Sau khi `bundle install` thì tạo file `.rubocop.yml`, `.slim-lint.yml`, `.reek`, trong thư mục root của dự án

### Rubocop

(Document)[https://github.com/rubocop-hq/rubocop]

**.rubocop.yml**
```yaml
require:
  - rubocop-performance
  - rubocop-rails

AllCops:
  TargetRubyVersion: 2.6
  # RuboCop has a bunch of cops enabled by default. This setting tells RuboCop
  # to ignore them, so only the ones explicitly set in this file are enabled.
  DisabledByDefault: true
  Exclude:
    - "**/tmp/**/*"
    - "**/templates/**/*"
    - "**/vendor/**/*"
    - "actionpack/lib/action_dispatch/journey/parser.rb"
    - "railties/test/fixtures/tmp/**/*"
    - "actionmailbox/test/dummy/**/*"
    - "actiontext/test/dummy/**/*"
    - "**/node_modules/**/*"
    - "Dangerfile"
    - "Gemfile"
    - "Gemfile.lock"
    - "Rakefile"
    - "db/schema.rb"
    - "db/migrate/*"
    - "config.ru"
    - "config/**/*"
    - "spec/*"
    - "test/**/*"
    - "db/*"
    - "bin/*"
    - "lib/task/seed_fu/custom_sql_writer.rb"
    - "db/fixtures/**/*"

Performance:
  Exclude:
    - "**/test/**/*"

# Prefer assert_not over assert !
Rails/AssertNot:
  Include:
    - "**/test/**/*"

# Prefer assert_not_x over refute_x
Rails/RefuteMethods:
  Include:
    - "**/test/**/*"

# Prefer &&/|| over and/or.
Style/AndOr:
  Enabled: true

# Align `when` with `case`.
Layout/CaseIndentation:
  Enabled: true

# Align comments with method definitions.
Layout/CommentIndentation:
  Enabled: true

Layout/ElseAlignment:
  Enabled: true

# Align `end` with the matching keyword or starting expression except for
# assignments, where it should be aligned with the LHS.
Layout/EndAlignment:
  Enabled: true
  EnforcedStyleAlignWith: variable
  AutoCorrect: true

Layout/EmptyLineAfterMagicComment:
  Enabled: true

Layout/EmptyLinesAroundAccessModifier:
  Enabled: true
  EnforcedStyle: only_before

Layout/EmptyLinesAroundBlockBody:
  Enabled: true

# In a regular class definition, no empty lines around the body.
Layout/EmptyLinesAroundClassBody:
  Enabled: true

# In a regular method definition, no empty lines around the body.
Layout/EmptyLinesAroundMethodBody:
  Enabled: true

# In a regular module definition, no empty lines around the body.
Layout/EmptyLinesAroundModuleBody:
  Enabled: true

# Use Ruby >= 1.9 syntax for hashes. Prefer { a: :b } over { :a => :b }.
Style/HashSyntax:
  Enabled: true

Layout/IndentFirstArgument:
  Enabled: true

# Method definitions after `private` or `protected` isolated calls need one
# extra level of indentation.
Layout/IndentationConsistency:
  Enabled: true
  EnforcedStyle: indented_internal_methods

# Two spaces, no tabs (for indentation).
Layout/IndentationWidth:
  Enabled: true

Layout/LeadingCommentSpace:
  Enabled: true

Layout/SpaceAfterColon:
  Enabled: true

Layout/SpaceAfterComma:
  Enabled: true

Layout/SpaceAfterSemicolon:
  Enabled: true

Layout/SpaceAroundEqualsInParameterDefault:
  Enabled: true

Layout/SpaceAroundKeyword:
  Enabled: true

Layout/SpaceBeforeComma:
  Enabled: true

Layout/SpaceBeforeComment:
  Enabled: true

Layout/SpaceBeforeFirstArg:
  Enabled: true

Style/DefWithParentheses:
  Enabled: true

# Defining a method with parameters needs parentheses.
Style/MethodDefParentheses:
  Enabled: true

Style/FrozenStringLiteralComment:
  Enabled: true
  EnforcedStyle: always
  Exclude:
    - "actionview/test/**/*.builder"
    - "actionview/test/**/*.ruby"
    - "actionpack/test/**/*.builder"
    - "actionpack/test/**/*.ruby"
    - "activestorage/db/migrate/**/*.rb"
    - "activestorage/db/update_migrate/**/*.rb"
    - "actionmailbox/db/migrate/**/*.rb"
    - "actiontext/db/migrate/**/*.rb"

Style/RedundantFreeze:
  Enabled: true

# Use `foo {}` not `foo{}`.
Layout/SpaceBeforeBlockBraces:
  Enabled: true

# Use `foo { bar }` not `foo {bar}`.
Layout/SpaceInsideBlockBraces:
  Enabled: true
  EnforcedStyleForEmptyBraces: space

# Use `{ a: 1 }` not `{a:1}`.
Layout/SpaceInsideHashLiteralBraces:
  Enabled: true

Layout/SpaceInsideParens:
  Enabled: true

# Check quotes usage according to lint rule below.
Style/StringLiterals:
  Enabled: true
  EnforcedStyle: single_quotes

# Detect hard tabs, no hard tabs.
Layout/Tab:
  Enabled: true

# Blank lines should not have any spaces.
Layout/TrailingBlankLines:
  Enabled: true

# No trailing whitespace.
Layout/TrailingWhitespace:
  Enabled: true

# Use quotes for string literals when they are enough.
Style/RedundantPercentQ:
  Enabled: true

Lint/AmbiguousOperator:
  Enabled: true

Lint/AmbiguousRegexpLiteral:
  Enabled: true

Lint/ErbNewArguments:
  Enabled: true

# Use my_method(my_arg) not my_method( my_arg ) or my_method my_arg.
Lint/RequireParentheses:
  Enabled: true

Lint/ShadowingOuterLocalVariable:
  Enabled: true

Lint/StringConversionInInterpolation:
  Enabled: true

Lint/UriEscapeUnescape:
  Enabled: true

Lint/UselessAssignment:
  Enabled: true

Lint/DeprecatedClassMethods:
  Enabled: true

Style/ParenthesesAroundCondition:
  Enabled: true

Style/RedundantBegin:
  Enabled: true

Style/RedundantReturn:
  Enabled: true
  AllowMultipleReturnValues: true

Style/Semicolon:
  Enabled: true
  AllowAsExpressionSeparator: true

# Prefer Foo.method over Foo::method
Style/ColonMethodCall:
  Enabled: true

Style/TrivialAccessors:
  Enabled: true

Performance/FlatMap:
  Enabled: true

Performance/RedundantMerge:
  Enabled: true

Performance/StartWith:
  Enabled: true

Performance/EndWith:
  Enabled: true

Performance/RegexpMatch:
  Enabled: true

Performance/ReverseEach:
  Enabled: true

Performance/UnfreezeString:
  Enabled: true
```

**Thực thi rubocop**

Chạy rubocop không đối số để kiểm tra tất cả các file Ruby ở trong thư mục hiện tại. `rubocop`

Chạy riêng 1 thư mục `rubocop app/`

Chạy riêng 1 file `rubocop app/models/user.rb`

Hoặc có thể chạy đồng thời các thư mục và các file khác nhau `rubocop app/models/user.rb app/controllers/ app/views/test/index.rb`

Muốn autofix thì thêm option `-a`

### Slim lint

[Document](https://github.com/sds/slim-lint)

**.slim-lint.yml**
```yaml
# Default application configuration that all configurations inherit from.
#
# This is an opinionated list of which hooks are valuable to run and what their
# out of the box settings should be.

# Whether to ignore frontmatter at the beginning of Slim documents for
# frameworks such as Jekyll/Middleman
skip_frontmatter: false

linters:
  CommentControlStatement:
    enabled: true

  ConsecutiveControlStatements:
    enabled: true
    max_consecutive: 2

  ControlStatementSpacing:
    enabled: true

  EmptyControlStatement:
    enabled: true

  EmptyLines:
    enabled: true

  FileLength:
    enabled: false
    max: 300

  LineLength:
    enabled: true
    max: 180

  RedundantDiv:
    enabled: true

  RuboCop:
    enabled: true
    # These cops are incredibly noisy since the Ruby we extract from Slim
    # templates isn't well-formatted, so we ignore them.
    # WARNING: If you define this list in your own .slim-lint.yml file, you'll
    # be overriding the list defined here.
    ignored_cops:
      - Layout/AlignArguments
      - Layout/AlignArray
      - Layout/AlignHash
      - Layout/AlignParameters
      - Layout/EmptyLineAfterGuardClause
      - Layout/FirstParameterIndentation
      - Layout/IndentArray
      - Layout/IndentationConsistency
      - Layout/IndentationWidth
      - Layout/InitialIndentation
      - Layout/MultilineArrayBraceLayout
      - Layout/MultilineAssignmentLayout
      - Layout/MultilineHashBraceLayout
      - Layout/MultilineMethodCallBraceLayout
      - Layout/MultilineMethodCallIndentation
      - Layout/MultilineMethodDefinitionBraceLayout
      - Layout/MultilineOperationIndentation
      - Layout/TrailingBlankLines
      - Layout/TrailingWhitespace
      - Lint/BlockAlignment
      - Lint/EndAlignment
      - Lint/Void
      - Metrics/BlockLength
      - Metrics/BlockNesting
      - Metrics/LineLength
      - Naming/FileName
      - Style/FrozenStringLiteralComment
      - Style/IfUnlessModifier
      - Style/Next
      - Style/WhileUntilModifier

  Tab:
    enabled: true

  TagCase:
    enabled: true

  TrailingBlankLines:
    enabled: true

  TrailingWhitespace:
    enabled: true
```

**Thực thi slim-lint**

Cho folder cụ thể `slim-lint app/views/`
Cho những file slim trong thư mục app: `slim-lint app/**/*.slim`

### Reek code smell

(Document)[https://github.com/troessner/reek]

```yaml
#https://github.com/troessner/reek#working-with-rails
directories:
  "app/controllers":
    IrresponsibleModule:
      enabled: false
    NestedIterators:
      max_allowed_nesting: 2
    UnusedPrivateMethod:
      enabled: false
    InstanceVariableAssumption:
      enabled: false
  "app/helpers":
    IrresponsibleModule:
      enabled: false
    UtilityFunction:
      enabled: false
  "app/mailers":
    InstanceVariableAssumption:
      enabled: false
  "app/models":
    InstanceVariableAssumption:
      enabled: false

### Excluding directories
# Directories and files below will not be scanned at all
exclude_paths:
  - db/migrate
  - db/fixtures/
  - vendor/bundle/
```
