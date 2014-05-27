redmine_smile_togglesidebar
===========================

Redmine plugin that adds a button to hide the right sidebar

# How it works

It stores a session cookie for each controller, to memorize the state of the sidebar

# To enable the + / - button, edit the file app/views/layouts/base.html.erb (or base.rhtml for older versions)

## 1) Replace this line :
```erb
<div id="main" class="<%= sidebar_content? ? '' : 'nosidebar' %>">
```

With :
```erb
<%
  show_sidebar = sidebar_content?
  if self.respond_to?('session_name_show_sidebar')
    session_show_sidebar = session[session_name_show_sidebar(controller_name, action_name)]
    session_show_sidebar = true if session_show_sidebar.nil?
    show_sidebar &&= session_show_sidebar
  end
%>
<div id="main" class="<%= (show_sidebar ? '' : 'nosidebar') %>">
```

## 2) After the following line :
```erb
<pre>
  <div id="content"> 
```

Add this piece of code :
```erb
<% if has_content?(:sidebar) && self.respond_to?('button_toggle_sidebar') -%>
    <div id="toggle-sidebar" style="float: right; position: relative; margin-left: 4px">
      <%= button_toggle_sidebar(false, false, false) %>
  </div>
<% end -%>
```
