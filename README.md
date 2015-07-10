# rails_console_exercises
## Console Lab

For this exercise, you will be practicing your Rails console skills. Write out the console commands you would use to execute these queries

### To Start

1. Fork and clone the readme or create your own readme where you will place your answers
2. Create a new rails application (don't forget to `cd` into the directory)
3. Add `pry-rails` to your `Gemfile` and run `bundle install`
4. Make sure you have created your database
1. Generate a model called Student, that has a first_name, last_name and age
2. Don't forget to run your migrations

### Tasks to create

####1. Using the new/save syntax, create a student with a first and last name and an age

2.2.1 :003 > anotherStudent = Student.new(first_name: "Andrew", last_name: "Moreno", age: 21)
 => #<Student id: nil, first_name: "Andrew", last_name: "Moreno", age: 21, created_at: nil, updated_at: nil>

####2. Save the student to the database
 
2.2.1 :004 > anotherStudent.save
   (0.2ms)  BEGIN
  SQL (0.4ms)  INSERT INTO "students" ("first_name", "last_name", "age", "created_at", "updated_at") VALUES ($1, $2, $3, $4, $5) RETURNING "id"  [["first_name", "Andrew"], ["last_name", "Moreno"], ["age", 21], ["created_at", "2015-07-10 07:20:09.599067"], ["updated_at", "2015-07-10 07:20:09.599067"]]
   (1.4ms)  COMMIT
 => true

####3. Using the find/set/save syntax update the student's first name to Myles

2.2.1 :007 > result = Student.find(2)
  Student Load (0.5ms)  SELECT  "students".* FROM "students" WHERE "students"."id" = $1 LIMIT 1  [["id", 2]]
 => #<Student id: 2, first_name: "Andrew", last_name: "Moreno", age: 21, created_at: "2015-07-10 07:20:09", updated_at: "2015-07-10 07:20:09">
2.2.1 :008 > result.update_attributes(first_name: "Myles")
   (0.2ms)  BEGIN
  SQL (0.3ms)  UPDATE "students" SET "first_name" = $1, "updated_at" = $2 WHERE "students"."id" = $3  [["first_name", "Myles"], ["updated_at", "2015-07-10 07:26:54.280679"], ["id", 2]]
   (1.2ms)  COMMIT
 => true
2.2.1 :009 > result.save
   (0.2ms)  BEGIN
   (0.2ms)  COMMIT
 => true

####4. Delete the student (where first_name is Myles)

2.2.1 :010 > result.destroy
   (0.2ms)  BEGIN
  SQL (0.4ms)  DELETE FROM "students" WHERE "students"."id" = $1  [["id", 2]]
   (1.4ms)  COMMIT
 => #<Student id: 2, first_name: "Myles", last_name: "Moreno", age: 21, created_at: "2015-07-10 07:20:09", updated_at: "2015-07-10 07:26:54"> 

####5. In your model, validate that every Student's last name is unique

validates_uniqueness_of: last_name

####6. In your model, validate that every Student has a first and last name that is longer than 4 characters

validates: :first_name,
          presence: true,
          length: {minimum: 5},
          numericality: false
  
validates: :last_name,
          presence: true,
          length: {minimum: 5},
          numericality: false

####7. Validate that every first and last name cannot be empty



####8. Create a migration that adds a column with a type of string called favorite_color to the students table (don't forget to run `rake db:migrate` after and for this question write the command in terminal to generate this migration)
####8. Using the create syntax create a student named John Doe who is 23 years old and has a favorite_color of purple
####9. Show if this new student entry is valid
####10. Show the number of errors for this student instance
####11. Using update, Change John Doe's name to Martin Fowler
####13. Save Martin Fowler
####15. Find all of the Students
####16. Find the student with an ID of 128 and if it does not exist, make sure it returns nil and not an error
####17. Find the first student in the table
####18. Find the last student in the table
####19. Find the student with the last name of Fowler
####20. Find all of students who have the first name of Martin and a favorite color of red
####21. Find all of the students and limit the search to 5 students, starting with the 2nd student and finally, order the students in alphabetical order
####20. Delete Martin Fowler (but first look up who he is!)
####21. Delete all of the students

### Bonus
1. Use the validates_format_of and regex to only validate names that consist of letters (no numbers or symbols) and start with a capital letter
2. Write a custom validation to ensure that no one named Elie Schoppik, Colt Steele or Tim Garcia is included in the students table.

