---
layout: post
title:      "Sinatra Project -Movie Reviewer"
date:       2019-09-26 16:12:27 +0000
permalink:  sinatra_project_-movie_reviewer
---


For my second project I chose to do continue along the same lines of my CLI project and do a Movie Review app. My intention was for a user to sign up/log in and then they would be taken to the homepage where they could see all the movie reviews. Here they could add a review and only they could edit or delete their reviews. 

In order to implement the features I wants I had to create helper methods that I could call in my controllers to make sure that users were logged in, and only had editing/deleting access to their reviews. 

``` helpers do

  def logged_in?
    !!current_user
  end

  def current_user
    @current_user ||= User.find(session[:user_id]) if session[:user_id]
  end
end ```

The current_user method here is looking for a User’s session id if a session has been started. It will then assign that user to the variable @current_user if @current_user hasn’t been assigned already in this session. This puts less strain on the database when looking for users. 

In the logged_in? method we use the double bang (!!) in order to return a true value. In this case we know someone is logged in if they are a current_user. 

