# Code Organization

As a file's size grows with continued development, it is important to logically group
methods, macros, constants, and more to maintain readability. Below are examples of how Red Nova Labs expects files and projects to be organized. Some of these requirements are enforced by pull request [status checks](https://help.github.com/articles/about-required-status-checks/) on GitHub now or will be in the future.

## Ruby on Rails

The structure of a Ruby on Rails project is defined by the framework itself, as outlined [here](http://guides.rubyonrails.org/getting_started.html). Red Nova Labs adheres to this predefined structure with some exceptions. This section of the guide is focused more on how certain types of files within a Rails project should be formatted.

### Controller File Organization

```ruby
class PersonsController < ApplicationController
  # Includes
  include Authenticatable

  # Layout
  layout 'facility'

  # Macros
  supports_pjax
  cache_sweeper :root_sweeper
  protect_from_forgery with: :exception

  # Actions
  before_action :authenticate_user

  # GET /
  def index
  end

  # POST /
  def create
  end

  # GET /new
  def new
  end

  # GET /:id/edit
  def edit
  end

  # GET /:id
  def show
  end

  # PUT /:id
  # PATCH /:id
  def update
  end

  # DELETE /:id
  def destroy
  end

  # Protected and Private Methods

  protected

  def some_protected_method
  end

  private

  def some_private_method
  end
end
```

### Model File Organization

A mix of bbatsov's [Ruby](https://github.com/bbatsov/ruby-style-guide#classes--modules) and [Rails](https://github.com/bbatsov/rails-style-guide#macro-style-methods) file organization guides.

```ruby
class User
  # Default Scope
  default_scope { where(active: true) }

  # Extends and Includes
  extend SomeModule
  include AnotherModule

  # Inner Classes
  CustomError = Class.new(StandardError)

  # Constants
  SOME_CONSTANT = 20

  # Attribute Macros
  attr_reader :name
  attr_accessor :formatted_date_of_birth

  # Enums
  enum gender: { female: 0, male: 1 }

  # Association Macros
  belongs_to :country
  has_many :authentications, dependent: :destroy

  # Validation Macros
  validates :email, presence: true
  validates :username, presence: true
  validates :username, uniqueness: { case_sensitive: false }
  validates :username, format: { with: /\A[A-Za-z][A-Za-z0-9._-]{2,19}\z/ }
  validates :password, format: { with: /\A\S{8,128}\z/, allow_nil: true }

  # Callbacks
  before_save :cook
  before_save :update_username_lower

  # Other Macros
  devise :database_authenticatable

  # Public Class Methods
  def self.some_method
  end

  # Initializer
  def initialize
  end

  # Public Instance Methods
  def some_method
  end

  # Protected and Private Methods

  protected

  def some_protected_method
  end

  private

  def some_private_method
  end
end
```

#### Model Test File Organization

A model's test file should mostly mirror the organization present in the model itself. `describe` and `context` blocks should be used instead of comments to provide information about the file's structure and code grouping.

```ruby
describe User do
  describe('Default Scope') do
    context('when performing a query') do
      it('returns only active Users by default') do
        ...
      end
    end
  end

  describe('Inner Classes') do
    describe('CustomError') do
      it('inherits from StandardError') do
        ...
      end
    end
  end

  describe('Constants') do
    it('has a constant for doing something specific') do
      ...
    end
  end

  describe('Attribute Macros') do
    it('makes name readable') do
      ...
    end
  end

  describe('Enums') do
    it('has gender saved as an enumerator') do
      ...
    end
  end

  describe('Association Macros') do
    it('belongs to a country') do
      ...
    end
  end

  describe('Validation Macros') do
    it('validates the presence of an email') do
      ...
    end
  end

  describe('Callbacks') do
    context('before_save') do
      it('lowercases the username attribute') do
        ...
      end
    end
  end

  describe('Other Macros') do
    it('authenticates through Devise') do
      ...
    end
  end

  describe('Public Class Methods') do
    describe('.some_method') do
      it('does a thing') do
        ...
      end
    end
  end

  describe('Initializer') do
    it('derives full_name from first_name and last_name') do
      ...
    end
  end

  describe('Public Instance Methods') do
    describe('#some_method') do
      it('does a thing') do
        ...
      end
    end
  end
end
```
