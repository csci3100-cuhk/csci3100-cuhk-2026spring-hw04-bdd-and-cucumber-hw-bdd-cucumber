# Add a declarative step here for populating the DB with movies.

Given(/the following movies exist/) do |movies_table|
  movies_table.hashes.each do |movie|
    Movie.create!(
      title: movie['title'],
      rating: movie['rating'],
      release_date: Time.zone.parse(movie['release_date'])
    )
  end
end

Then(/(.*) seed movies should exist/) do |n_seeds|
  expect(Movie.count).to eq n_seeds.to_i
end

# Make sure that one string (regexp) occurs before or after another one
#   on the same page

Then(/^I should see "(.*)" before "(.*)" in the movie list$/) do |movie1, movie2|
  pattern = /#{Regexp.escape(movie1)}.*#{Regexp.escape(movie2)}/m
  expect(page.body).to match(pattern)
end


# Make it easier to express checking or unchecking several boxes at once
#  "When I uncheck the following ratings: PG, G, R"
#  "When I check the following ratings: G"

When(/I check the following ratings: (.*)/) do |rating_list|
  # first, uncheck all the boxes
  %w[G PG PG-13 R].each do |rating|
    uncheck("ratings[#{rating}]")
  end
  # now check the selected ones
  rating_list.split(/\s*,\s*/).each do |rating|
    check("ratings[#{rating}]")
  end
end

# Part 2, Step 3
Then(/^I should (not )?see the following movies: (.*)$/) do |no, movie_list|
  movie_list.split(/\s*,\s*/).each do |movie|
    if no
      expect(page).to_not have_content(movie)
    else
      expect(page).to have_content(movie)
    end
  end
end

Then(/^I should see all the movies$/) do
  # Make sure that all the movies in the app are visible in the table
  all_titles = Movie.all.pluck(:title).join(', ')
  steps %(
  Then I should see the following movies: #{all_titles}
)
end

### Utility Steps Just for this assignment.

Then(/^debug$/) do
  # Use this to write "Then debug" in your scenario to open a console.
  require "byebug"
  byebug
  1 # intentionally force debugger context in this method
end

Then(/^debug javascript$/) do
  # Use this to write "Then debug" in your scenario to open a JS console
  page.driver.debugger
  1
end

Then(/complete the rest of of this scenario/) do
  # This shows you what a basic cucumber scenario looks like.
  # You should leave this block inside movie_steps, but replace
  # the line in your scenarios with the appropriate steps.
  raise "Remove this step from your .feature files"
end
