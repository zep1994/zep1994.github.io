---
layout: post
title:      "The Rails Portfolio Project"
date:       2018-11-12 20:48:31 +0000
permalink:  the_rails_portfolio_project
---


This project was by far the most difficult one yet. I spent about 12 hours a day working on this project and progress was slow. Although it was difficult, I finally am starting to feel more comfortable with setting up the associations in the controller. I still feel like I have much to learn about this, but I completed this project and feel good about the work I have done. Here are some things I learned while doing this project. I will use an example to cover this topic. First, I want to talk about creating an instance of an object that is associated with another object. The hard part for me, is how to create this object using methods I must define in the controller. Well, this is where I really earned my PHD in googling. I had three models, team, player, and assignments. How do I create a team that can have players assigned to it. I first had to set up the abilty to create a team. I just used the standard way of setting up the new and create methods with strong params to whitelist the attributes at the bottm. Thats great, but how do I associate assignments with this. Before going and further, I should mention that I already set up the create actions and strong params for players and assignments as well. The assignments needed to be associated with team and player. So, to do this I added player_id and team_id to assignment_params.  This way when I called the create method, assignments knew what it was associated to, but still teams does not know about assignments. So jumping back to the teams controler I needed to add assignments to the team params. Since teams has_many assignments, I set up an empty array in the team params to collect all the ids of the assignments being added to that specific instance of a team. Although, at this point, teams still needs to know what the attributes are for assignments. I could not just add,

`:assignments_attributes=>[:name, :description, :player_id, :team_id]`

I need to also add  a method to the teams model that would itterate over the attributes and build them as needed. I used a method, that is covered in the rails docs. https://guides.rubyonrails.org/association_basics.html#has-many-association-reference

```
def assignments_attributes=(assignments_attributes)
      assignments_attributes.values.each do |assignment_attributes|
          if assignment_attributes[:team_id] != ""
              assignment = Assignment.find_or_create_by(assignment_attributes)
              if !self.assignments.include?(assignment)
                  self.assignments.build(assignment_attributes)
              end
          end
      end
  end
```
Here I am defing assignment_attributes so I can use that in the teams controller. By using this method, I can ensure that the objects are persisted in the database. you can see on line 2, that I am itterating over the values of each attribute and then checking to see if the team with a team_id is equal to "",  if it is this will fire off the fourth line where I will find or create by the assignment_attributes. Now if the assignments (becaue a team has many assignments) does not include assignment, we will simply build the assignment_attributes. At this point, I should mention, that I could have been wrong about something and please reach out to me if you find something I should fix. Moving on, I can now use assignment_attributes in the teams controller. So now when I create the team object an assignment will be associated with it. We are not done yet though. I need to express this in a view so a user can actually do this, because using the rails console is just not logical. 

This part drove me crazy I think. Let me show you the code that made it possible and then I will go over it. 
```
<h1>New Team Form</h1>
<div class="team_form">
<%= form_for @team do |f| %>
    <%= f.label :name %>
    <%= f.text_field :name %><br>
    <%= f.label :type_player, "Type Team" %>
    <%= f.text_field :type_player %><br>
    <%= f.label :role, "Goals" %>
    <%= f.text_field :role %><br>
    <%= f.label :quote %>
    <%= f.text_field :quote %><br>

    <p>Create Assignment?</p>
    <%= f.fields_for :assignments, @team.assignments.build do |a| %>

        <p>Select a team member:
        <%= select_tag 'team[assignments_attributes][0][player_id]', content_tag(:option,'select one...',:value=>"")+options_from_collection_for_select(Player.all, :id, :name) %></p>

        <%= a.hidden_field :team_id, value: @team.id %>

        <%= a.label :name, "Assignment Name" %>
        <%= a.text_field :name %><br>
        <%= a.label :description %>
        <%= a.text_field :description %>
    <% end %>
    <br>
    <%= f.submit %>
<% end %>
```
You can see at the top that I am creating a team and halfway down I am creating the assignment. I used fields_for, because I wanted to specify additional model objects in the same form. So by using :assignments, @team.assignments.build I can associated this form with the given team and build the new objects and have them associated with team. Now I learned a little trick here, see the hidden_field? It contains :team_id with a value of @team.id. This will not appear on the page, but it is in the HTML. It is appended onto the a, which is associated with the assignments. So now the form can find the specific team that this form will try to submit to.  So with some sanity regained, I can get ready for my assessment, which makes me so nervous, because I freeze up and forget everything when someone is watching. I admit this stuff is only starting to be engrained in my head and everything is not so clear just yet, but after the assessments I find I feel much more confident in my skills and then everything starts to become very clear. So I hope that happens this time! What a long strange trip its been going over all this stuff but sooo worth it. 
