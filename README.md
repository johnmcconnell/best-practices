# best-practices
A guide of my best practices

## Best Practices

### 1. A test belongs in the same package/namespace as the source code it is testing

For example, an application that has the directory structure below:

```
  src
   |-erebos
         |- convolution.clj
         |- ica.clj
         |- pca.clj
         |- main.clj
```

should have tests in:

```
  test
   |-erebos
         |- convolution_test.clj
         |- ica_test.clj
         |- pca_test.clj
```

### 2. Keep line length short

Code which looks like:

```ruby
def application_keywords(params)
  id = params.fetch(:id)
  user = params.fetch(:user)
  app = find_application(id)
  documents = app.docs
  if user.legal_scoped?
    documents = app.build_legal_docs(Time.now, user)
  end
  semantic_keywords(documents)
end
```

is preferred over
```ruby
def application_keywords(params)
  semantic_keywords(if params.fetch(:user).legal_scoped? then find_application(params.fetch(:id)).build_legal_docs(Time.now, params.fetch(:user)) else find_application(params.fetch(:id)).docs
end
```

You can add this to your .vimrc to highlight the 80th column.

http://stackoverflow.com/questions/235439/vim-80-column-layout-concerns
```
if exists('+colorcolumn')
  set colorcolumn=80
else
  au BufWinEnter * let w:m2=matchadd('ErrorMsg', '\%>80v.\+', -1)
endif
```

### 3. Affirmative predicates are more readable

There are two different types of predicates; affirmative and negative.

For example, `valid?` is affirmative and `not_valid?` is negative.

Code which looks like:

```ruby
if not valid?
```

is preferred over

```
if not_valid?
```

If requirements change and the logic needs to be complemented.
The following code looks much better:

```
if valid?
```

over

```
if not not_valid?
```

### 4. Predicate functions should have a '?' suffix

Predicate functions should have a `?` suffix (when possible).

For example:

```ruby
def valid?
```

is preferred over

```ruby
def valid
```

### 5. Functions with side effects should have a '!' suffix

Functions with side effects should have a `!` suffix (when possible).
Side effects include IO, system calls, interacting with global state,
and calling another function with side effects.

For example:

```ruby
def fetch_from_db!
```

is preferred over

```ruby
def fetch_from_db
```

### 6. Use a package structure centered around the domain

A project should have a directory structure centered around its problem domain.
For example, an application that has the directory structure below:

```
 src
  |- task
       |- handler.clj
       |- db.clj
       |- domain.clj
       |- runner.clj
  |- label
       |- handler.clj
       |- db.clj
       |- domain.clj
       |- runner.clj
  |- item
       |- handler.clj
       |- db.clj
       |- domain.clj
       |- runner.clj
```

is preferred over

```
 src
  |- handlers
       |- task.clj
       |- label.clj
       |- item.clj
  |- dbs
       |- task.clj
       |- label.clj
       |- item.clj
  |- domains
       |- task.clj
       |- label.clj
       |- item.clj
  |- runners
       |- task.clj
       |- label.clj
       |- item.clj
```

## License

Copyright © 2017 John McConnell

Distributed under the MIT License
