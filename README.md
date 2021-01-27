# Happy has many
## Baseline Hanami
1. `hanami new hanami-has-many`
    - Note this created a directory named `hanami_has_many`
1. `bundle install`
1. Run tests, they work: `bundle exec rake`
1. `git add <bunch-o-stuff>`
1. `git commit -av -m 'bundle install'`

## Add model and association
1. `bundle exec hanami generate model author`
1. `bundle exec hanami generate model book`
1. `git commit`
1. Edit author migration: https://guides.hanamirb.org/associations/has-many/
    - This adds one line: `column :name,       String,   null: false`
1. Edit book migration based on same link; this adds two lines:
    - `foreign_key :author_id, :authors, on_delete: :cascade, null: false`
    - `column :title,      String,   null: false`
1. Prepare DBs:
    - Dev: `bundle exec hanami db prepare`
    - Test: `HANAMI_ENV=test bundle exec hanami db prepare`
1. Edit the author repository: https://guides.hanamirb.org/associations/has-many/#basic-usage
1. Test in console: `bundle exec hanami console --engine=pry`
    - `author_repository = AuthorRepository.new`
    - `author = author_repository.create_with_books(name: "Alexandre Dumas", books: [{title: "The Count of Montecristo"}])`
    - `author.name`
    - `author.id`
    - `author.books` # lists books!
    - `author = author_repository.find(author.id)`
    - `author.books` # Does NOT list books!
    - `author = author_repository.find_with_books(author.id)`
    - `author.books` # lists books!
1. Test and commit
1. Edit the author repository again: https://guides.hanamirb.org/associations/has-many/#add-and-remove
1. Test in console: `bundle exec hanami console --engine=pry`
    - `author_repository = AuthorRepository.new`
    - `author = author_repository.find_with_books(1)`
    - `book = author_repository.add_book(author, title: "The Three Musketeers")`
    - `author_repository.remove_book(author, book.id)`

# Hanami Has Many

Welcome to your new Hanami project!

## Setup

How to run tests:

```
% bundle exec rake
```

How to run the development console:

```
% bundle exec hanami console
```

How to run the development server:

```
% bundle exec hanami server
```

How to prepare (create and migrate) DB for `development` and `test` environments:

```
% bundle exec hanami db prepare

% HANAMI_ENV=test bundle exec hanami db prepare
```

Explore Hanami [guides](https://guides.hanamirb.org/), [API docs](http://docs.hanamirb.org/1.3.3/), or jump in [chat](http://chat.hanamirb.org) for help. Enjoy! 🌸
