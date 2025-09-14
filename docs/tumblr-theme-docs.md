## Contents[Introduction](https://www.tumblr.com/docs/en/custom_themes#introduction)  
[Get Started](https://www.tumblr.com/docs/en/custom_themes#get_started)  
[Basic Variables](https://www.tumblr.com/docs/en/custom_themes#basic_variables)  
[Global Appearance](https://www.tumblr.com/docs/en/custom_themes#global_appearance)  
[Navigation](https://www.tumblr.com/docs/en/custom_themes#navigation)  
[Posts](https://www.tumblr.com/docs/en/custom_themes#posts)  
[Reblogs](https://www.tumblr.com/docs/en/custom_themes#reblogs)  
[Neue Post Format](https://www.tumblr.com/docs/en/custom_themes#npf)  
[Legacy Posts](https://www.tumblr.com/docs/en/custom_themes#text-posts)  
[Text Posts](https://www.tumblr.com/docs/en/custom_themes#text-posts)  
[Photo Posts](https://www.tumblr.com/docs/en/custom_themes#photo-posts)  
[Panorama Posts](https://www.tumblr.com/docs/en/custom_themes#panorama-posts)  
[Photoset Posts](https://www.tumblr.com/docs/en/custom_themes#photoset-posts)  
[Quote Posts](https://www.tumblr.com/docs/en/custom_themes#quote-posts)  
[Link Posts](https://www.tumblr.com/docs/en/custom_themes#link-posts)  
[Chat Posts](https://www.tumblr.com/docs/en/custom_themes#chat-posts)  
[Audio Posts](https://www.tumblr.com/docs/en/custom_themes#audio-posts)  
[Video Posts](https://www.tumblr.com/docs/en/custom_themes#video-posts)  
[Answer Posts](https://www.tumblr.com/docs/en/custom_themes#answer-posts)  
[Dates](https://www.tumblr.com/docs/en/custom_themes#dates)  
[Notes](https://www.tumblr.com/docs/en/custom_themes#notes)  
[Tags](https://www.tumblr.com/docs/en/custom_themes#tags)  
[Content Sources](https://www.tumblr.com/docs/en/custom_themes#content-sources)  
[Submissions](https://www.tumblr.com/docs/en/custom_themes#submissions)  
[Group Blogs](https://www.tumblr.com/docs/en/custom_themes#group-blogs)  
[Day Pages](https://www.tumblr.com/docs/en/custom_themes#day-pages)  
[Tag Pages](https://www.tumblr.com/docs/en/custom_themes#tag-pages)  
[Localization](https://www.tumblr.com/docs/en/custom_themes#localization)  
[Search](https://www.tumblr.com/docs/en/custom_themes#search)  
[Featured Tags](https://www.tumblr.com/docs/en/custom_themes#featured-tags)  
[Following](https://www.tumblr.com/docs/en/custom_themes#following)  
[Likes](https://www.tumblr.com/docs/en/custom_themes#likes)  
[Like and Reblog buttons](https://www.tumblr.com/docs/en/custom_themes#like_and_reblog_buttons)  
[Related Posts](https://www.tumblr.com/docs/en/custom_themes#related-posts)  
[Theme Options](https://www.tumblr.com/docs/en/custom_themes#theme-options)  
[Theme Assets](https://www.tumblr.com/docs/en/custom_themes#theme-assets)  
[Mobile Themes](https://www.tumblr.com/docs/en/custom_themes#mobile-themes)  
[Variable Transformations](https://www.tumblr.com/docs/en/custom_themes#variable-transformations)

# How to create a custom HTML theme 

Want to create a custom look for your blog? If you're comfortable hand-coding HTML, then you've come to the right place! If not, choose from hundreds of beautiful themes in the [Theme Garden](https://www.tumblr.com/themes).

## Introduction

Tumblr was originally built around seven key post types: text, photos, links, quotes, chat, audio, and video. Starting in 2018, we transitioned most new posts to using the [Neue Post Format](https://github.com/tumblr/docs/blob/master/npf-spec.md) to define content. These new "NPF" posts do not have a post type, as each post can now have a variety of content blocks. For backwards compatibility, these posts are represented as the legacy text post type in your blog theme, but you can get the NPF representation of any post for your theme (more on this in the ["Posts"](https://www.tumblr.com/docs/en/custom_themes#posts) section). We still support the old post types for legacy posts, so you should make sure your theme makes these beautiful.

For updates on new features, changes, and bugs we've resolved, visit our [Changes](https://changes.tumblr.com/) blog.

## Get Started

1. Click the name of your blog at the top of the Dashboard or under the list icon at the top.
2. Click "Customize" on the right column.
3. Click "Edit HTML" below the theme thumbnail on the left.

Want to learn more about our Customizer? Check out our Help Center article on [Customizing your Theme](https://help.tumblr.com/hc/articles/230775027-Customize-menu).

Tumblr has two types of special operators used to render content in your HTML.

**Variables** are used to insert dynamic data like your blog's title or description:

#### Example
    
    <html> <head> <title>**{Title}**</title> </head> <body> ... </body> </html>

**Blocks** are either used to render a block of HTML for a set of data (like your posts), or to conditionally render a block of HTML (like a "Previous Page" link):
    
    <html> <body> <ol id="posts">**{block:Posts}** <li> ... </li>**{/block:Posts}** </ol> </body> </html>

Here's an example of the complete markup for a theme:
    
    <html> <head> <title>{Title}</title> <link rel="shortcut icon" href="{Favicon}"> <link rel="alternate" type="application/rss+xml" href="{RSS}"> {block:Description} <meta name="description" content="{MetaDescription}" /> {/block:Description} </head> <body> <h1>{Title}</h1> {block:Description} <p id="description">{Description}</p> {/block:Description} <div id="posts"> {block:Posts} <!--NPF & Legacy Text Posts--> {block:Text} <div class="post text"> {block:Title} <h3><a href="{Permalink}">{Title}</a></h3> {/block:Title} <!--Original Post--> {block:NotReblog} {Body} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} <div class="reblog-list"> {block:Reblogs} <div class="reblog-header"> {block:IsActive} <a href="{Permalink}">{Username}</a> {/block:IsActive} {block:IsDeactivated} <span>{Username}</span> {/block:IsDeactivated} </div> <div class="reblog-body">{Body}</div> {/block:Reblogs} </div> {/block:RebloggedFrom} </div> {/block:Text} <!--All Answer posts including NPF--> {block:Answer} <div class="post answer"> <p><strong>{Asker}</strong> asked:</p> {Question} {block:Answerer} {Answer} {/block:Answerer} <!--Original Post--> {block:NotReblog} {Replies} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} <div class="reblog-list"> {block:Reblogs} <div class="reblog-header"> {block:IsActive} <a href="{Permalink}">{Username}</a> {/block:IsActive} {block:IsDeactivated} <span>{Username}</span> {/block:IsDeactivated} </div> <div class="reblog-body">{Body}</div> {/block:Reblogs} </div> {/block:RebloggedFrom} </div> {/block:Answer} <!--Legacy Photo Posts--> {block:Photo} <div class="post photo"> <img src="{PhotoURL-500}" alt="{PhotoAlt}"/> <!--Original Post--> {block:NotReblog} {Caption} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} <div class="reblog-list"> {block:Reblogs} <div class="reblog-header"> {block:IsActive} <a href="{Permalink}">{Username}</a> {/block:IsActive} {block:IsDeactivated} <span>{Username}</span> {/block:IsDeactivated} </div> <div class="reblog-body">{Body}</div> {/block:Reblogs} </div> {/block:RebloggedFrom} </div> {/block:Photo} <!--Legacy Photoset Posts--> {block:Photoset} <div class="post photoset"> {Photoset} <!--Original Post--> {block:NotReblog} {Caption} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} <div class="reblog-header"> {block:Reblogs} <div class="reblog-header"> {block:IsActive} <a href="{Permalink}">{Username}</a> {/block:IsActive} {block:IsDeactivated} <span>{Username}</span> {/block:IsDeactivated} </div> <div class="reblog-body">{Body}</div> {/block:Reblogs} </div> {/block:RebloggedFrom} </div> {/block:Photoset} <!--Legacy Quote Posts--> {block:Quote} <div class="post quote"> "{Quote}" {block:Source} <div class="source">{Source}</div> {/block:Source} </div> {/block:Quote} <!--Legacy Link Posts--> {block:Link} <div class="post link"> <a href="{URL}" class="link" {Target}>{Name}</a> <!--Original Post--> {block:NotReblog} {Description} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} <div class="reblog-list"> {block:Reblogs} <div class="reblog-header"> {block:IsActive} <a href="{Permalink}">{Username}</a> {/block:IsActive} {block:IsDeactivated} <span>{Username}</span> {/block:IsDeactivated} </div> <div class="reblog-body">{Body}</div> {/block:Reblogs} </div> {/block:RebloggedFrom} </div> {/block:Link} <!--Legacy Chat Posts--> {block:Chat} <div class="post chat"> {block:Title} <h3><a href="{Permalink}">{Title}</a></h3> {/block:Title} <ul class="chat"> {block:Lines} <li class="{Alt} user_{UserNumber}"> {block:Label} <span class="label">{Label}</span> {/block:Label}{Line} </li> {/block:Lines} </ul> </div> {/block:Chat} <!--Legacy Video Posts--> {block:Video} <div class="post video"> {Video-700} <!--Original Post--> {block:NotReblog} {Description} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} <div class="reblog-list"> {block:Reblogs} <div class="reblog-header"> {block:IsActive} <a href="{Permalink}">{Username}</a> {/block:IsActive} {block:IsDeactivated} span>{Username}</span> {/block:IsDeactivated} </div> <div class="reblog-body">{Body}</div> {/block:Reblogs} </div> {/block:RebloggedFrom} </div> {/block:Video} <!--Legacy Audio Posts--> {block:Audio} <div class="post audio"> {AudioEmbed} <!--Original Post--> {block:NotReblog} {Description} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} <div class="reblog-list"> {block:Reblogs} <div class="reblog-header"> {block:IsActive} <a href="{Permalink}">{Username}</a> {/block:IsActive} {block:IsDeactivated} <span>{Username}</span> {/block:IsDeactivated} </div> <div class="reblog-body">{Body}</div> {/block:Reblogs} </div> {/block:RebloggedFrom} </div> {/block:Audio} {/block:Posts} </div> <div id="footer"> {block:PreviousPage} <a href="{PreviousPage}">&larr; Previous</a> {/block:PreviousPage}{block:NextPage} <a href="{NextPage}">Next &rarr;</a> {/block:NextPage} <a href="/archive">Archive</a> </div> </body> </html> 

## Basic VariablesVariableDescription

{Title}The HTML-safe title of your blog.

{Description}The description of your blog. (may include HTML)

{MetaDescription}The HTML-safe description of your blog. 

e.g., `<meta name="description" content="{MetaDescription}" />`

{BlogURL}Main URL for your blog.

{RSS}RSS feed URL for your blog.

{Favicon}Favicon URL for your blog.

{CustomCSS}Any custom CSS code added on your [Customize](https://www.tumblr.com/customize) page.

{block:PermalinkPage} {/block:PermalinkPage}Rendered on post permalink pages. 

Useful for embedding comment widgets

{block:IndexPage} {/block:IndexPage}Rendered on index (post) pages.

{block:HomePage} {/block:HomePage}Rendered on the main post page.

{block:PostTitle}  
{PostTitle}  
{/block:PostTitle}Rendered on permalink pages. (Useful for displaying the current post's title in the page title) 

Example: `<title>{Title}{block:PostTitle} - {PostTitle}{/block:PostTitle}</title>`

{block:PostSummary}  
{PostSummary}  
{/block:PostSummary}Identical to `{PostTitle}`, but will automatically generate a summary if a title doesn't exist.

{PortraitURL-16}Portrait photo URL for your blog. 16-pixels by 16-pixels.

{PortraitURL-24}Portrait photo URL for your blog. 24-pixels by 24-pixels.

{PortraitURL-30}Portrait photo URL for your blog. 30-pixels by 30-pixels.

{PortraitURL-40}Portrait photo URL for your blog. 40-pixels by 40-pixels.

{PortraitURL-48}Portrait photo URL for your blog. 48-pixels by 48-pixels.

{PortraitURL-64}Portrait photo URL for your blog. 64-pixels by 64-pixels.

{PortraitURL-96}Portrait photo URL for your blog. 96-pixels by 96-pixels.

{PortraitURL-128}Portrait photo URL for your blog. 128-pixels by 128-pixels.

{CopyrightYears}Displays the span of years your blog has existed.

## Global Appearance

These template tags define custom colors, fonts, and other options that apply to your appearance on mobile devices and the [default theme](https://www.tumblr.com/theme/37310). VariableDescription

{TitleFont}The font used for your blog title.

{TitleFontWeight}The weight of your title font ("normal" or "bold").

{BackgroundColor}The background color of your blog.

{TitleColor}The title color of your blog.

{AccentColor}The accent color of your blog.

{HeaderImage}URL of your header image in all its glory. This will always have a value, even if it's a default header image.

{AvatarShape}The display shape of your avatar ("circle" or "square").

{block:ShowTitle} {/block:ShowTitle}Rendered if you have "Show title" enabled.

{block:HideTitle} {/block:HideTitle}Rendered if you have "Show title" disabled.

{block:ShowDescription} {/block:ShowDescription}Rendered if you have "Show description" enabled.

{block:HideDescription} {/block:HideDescription}Rendered if you have "Show description" disabled.

{block:ShowAvatar} {/block:ShowAvatar}Rendered if you have "Show avatar" enabled.

{block:HideAvatar} {/block:HideAvatar}Rendered if you have "Show avatar" disabled.

{block:ShowHeaderImage} {/block:ShowHeaderImage}Rendered if you have "Show header image" enabled.

{block:HideHeaderImage} {/block:HideHeaderImage}Rendered if you have "Show header image" disabled.

## NavigationVariableDescription

{block:Pagination}  
{/block:Pagination}Rendered if there is a "previous" or "next" page.

{block:PreviousPage}  
{/block:PreviousPage}Rendered if there is a "previous" page (newer posts) to navigate to.

{block:NextPage}  
{/block:NextPage}Rendered if there is a "next" page (older posts) to navigate to.

{PreviousPage}URL for the "previous" page (newer posts).

{NextPage}URL for the "next" page (older posts).

{CurrentPage}Current page number.

{TotalPages}Total page count.

{block:SubmissionsEnabled} {/block:SubmissionsEnabled}Rendered if Submissions are enabled.

{SubmitLabel}The customizable label for the Submit link. 

Example: "Submit"

{block:AskEnabled}  
{/block:AskEnabled}Rendered if asking questions is enabled.

{AskLabel}The customizable label for the Ask link. 

Example: "Ask me anything"

### Jump PaginationVariableDescription

{block:JumpPagination length="5"} {/block:JumpPagination}Rendered for each page _greater than the **current page** minus one-half **length**_ up to _**current page** plus one-half **length**_.

{block:CurrentPage} {/block:CurrentPage}Rendered when jump page is the current page.

{block:JumpPage} {/block:JumpPage}Rendered when jump page is _not_ the current page.

{PageNumber}Page number for jump page.

{URL}URL for jump page.

#### Example
    
    <html> <body> ... **{block:Pagination}****{block:PreviousPage}** <a href="**{PreviousPage}**">Previous</a> **{/block:PreviousPage}****{block:JumpPagination length="5"}****{block:CurrentPage}** <span class="current_page">**{PageNumber}**</span> **{/block:CurrentPage}****{block:JumpPage}** <a class="jump_page" href="**{URL}**">**{PageNumber}**</a> **{/block:JumpPage}****{/block:JumpPagination}****{block:NextPage}** <a href="**{NextPage}**">Next</a> **{/block:NextPage}****{/block:Pagination}** </body> </html>

### PagesVariableDescription

{block:HasPages} {/block:HasPages}Rendered if you have defined any custom pages.

{block:Pages} {/block:Pages}Rendered for each custom page.

{URL}The URL for this page.

{Label}The label for this page.

### Permalink NavigationVariableDescription

{block:PermalinkPagination}Rendered if there is a "previous" or "next" post.

{block:PreviousPost} {/block:PreviousPost}Rendered if there is a "previous" post to navigate to.

{block:NextPost} {/block:NextPost}Rendered if there is a "next" post to navigate to.

{PreviousPost}URL for the "previous" (newer) post.

{NextPost}URL for the "next" (older) post.

#### Example
    
    **{block:PermalinkPagination}**  **{block:PreviousPost}** <a href="**{PreviousPost}**">Previous Post</a> **{/block:PreviousPost}**   **{block:NextPost}** <a href="**{NextPost}**">Next Post</a> **{/block:NextPost}**  **{/block:PermalinkPagination}**

## PostsVariableDescription

{block:Posts} {/block:Posts}This block gets rendered for each post in reverse chronological order. The number of posts that appear per-page can be configured in the Customize area for the blog on the Advanced tab.

{block:Posts inlineMediaWidth="500"} {/block:Posts}Width for inline media in the post body. 

Minimum: 250px

{block:Posts inlineNestedMediaWidth="250"} {/block:Posts}Width for inline media in the reblog chain. 

Minimum: 250px (must be smaller than or same as inlineMediaWidth)

{block:Text} {/block:Text}Rendered for legacy Text posts and NPF posts.

{block:Answer} {/block:Answer}Rendered for Answer posts.

{block:Photo} {/block:Photo}Rendered for legacy Photo posts.

{block:Panorama} {/block:Panorama}Rendered for legacy Panorama posts.

{block:Photoset} {/block:Photoset}Rendered for legacy Photoset posts.

{block:Quote} {/block:Quote}Rendered for legacy Quote posts.

{block:Link} {/block:Link}Rendered for legacy Link posts.

{block:Chat} {/block:Chat}Rendered for legacy Chat posts.

{block:Audio} {/block:Audio}Rendered for legacy Audio posts.

{block:Video} {/block:Video}Rendered for legacy Video posts.

{PostType}The name of the current legacy post type.

{Permalink}The permalink for a post. 

Example: `"https://sample.tumblr.com/post/123"`

{RelativePermalink}The permalink for a post, but not including the domain. 

Example: `"/post/123"`

{ShortURL}A shorter URL that redirects to this post. 

Example: `"https://www.tumblr.com/xpv5qtavm"`

{EmbedUrl}URL of the embed page where users can copy the post's embed code. 

Example: `"https://sample.tumblr.com/post/123/embed"`

{PostID}The numeric ID for a post. 

Example: `1234567`

{TagsAsClasses}An HTML class-attribute friendly list of the post's tags. 

Example: `"humor office new_york_city"`  
By "HTML class-attribute friendly," we mean that it conforms to [HTML specifications for class-attributes](https://stackoverflow.com/questions/448981/what-characters-are-valid-in-css-class-selectors). Mostly, it should begin with a letter, followed by letters, digits, hyphens, or underscores. Letters need to be from the English alphabet, as international or non-English characters may give unexpected results. 

For posts imported from other sites, an HTML-friendly version of the source domain will also be included, with periods in the domain replaced by underscores. 

Example: `"twitter_com", "digg_com", etc.`  
The class-attribute "reblog" will be included automatically if the post was reblogged from another post.

{block:Post_\[1-15\]_} {/block:Post_\[1-15\]_}Rendered for the post at the specified offset. This makes it possible to insert an advertisement or design element in the middle of your posts. 

Example: `{block:Post5}`I'm the fifth post!`{/block:Post5}` will only be rendered on the fifth post being displayed.

{block:Odd} {/block:Odd}Rendered for every one of the current page's odd-numbered posts.

{block:Even} {/block:Even}Rendered for every one of the current page's even-numbered posts.

{block:More} {/block:More}Rendered on index pages for posts with Read More breaks.

{PostNotesURL}URL to an HTML partial of this post's [Notes](https://www.tumblr.com/docs/en/custom_themes#notes). Useful for loading Notes via AJAX.

{NPF}The [Neue Post Format](https://github.com/tumblr/docs/blob/master/npf-spec.md) JSON representation of the post, including its reblog trail, content, and layout information. Useful if you want to use Javascript to render your posts.

{block:PinnedPostLabel} {PinnedPostLabel} {/block:PinnedPostLabel}Label in post footer indicating this is a pinned post.

### ReblogsVariableDescription

{block:NotReblog} {/block:NotReblog}Rendered if a post was not reblogged from another post.

{block:RebloggedFrom} {/block:RebloggedFrom}Rendered if a post was reblogged from another post.

{ReblogParentName}The username of the blog this post was reblogged from.

{ReblogParentTitle}The title of the blog this post was reblogged from.

{ReblogParentURL}The URL for the blog this post was reblogged from.

{ReblogParentPortraitURL-16}Portrait photo URL for the blog this post was reblogged from. 16-pixels by 16-pixels.

{ReblogParentPortraitURL-24}Portrait photo URL for the blog this post was reblogged from. 24-pixels by 24-pixels.

{ReblogParentPortraitURL-30}Portrait photo URL for the blog this post was reblogged from. 30-pixels by 30-pixels.

{ReblogParentPortraitURL-40}Portrait photo URL for the blog this post was reblogged from. 40-pixels by 40-pixels.

{ReblogParentPortraitURL-48}Portrait photo URL for the blog this post was reblogged from. 48-pixels by 48-pixels.

{ReblogParentPortraitURL-64}Portrait photo URL for the blog this post was reblogged from. 64-pixels by 64-pixels.

{ReblogParentPortraitURL-96}Portrait photo URL for the blog this post was reblogged from. 96-pixels by 96-pixels.

{ReblogParentPortraitURL-128}Portrait photo URL for the blog this post was reblogged from. 128-pixels by 128-pixels.

{ReblogRootName}The username of the blog this post was created by.

{ReblogRootTitle}The title of the blog this post was created by.

{ReblogRootURL}The URL for the blog this post was created by.

{ReblogRootPortraitURL-16}Portrait photo URL for the blog this post was created by. 16-pixels by 16-pixels.

{ReblogRootPortraitURL-24}Portrait photo URL for the blog this post was created by. 24-pixels by 24-pixels.

{ReblogRootPortraitURL-30}Portrait photo URL for the blog this post was created by. 30-pixels by 30-pixels.

{ReblogRootPortraitURL-40}Portrait photo URL for the blog this post was created by. 40-pixels by 40-pixels.

{ReblogRootPortraitURL-48}Portrait photo URL for the blog this post was created by. 48-pixels by 48-pixels.

{ReblogRootPortraitURL-64}Portrait photo URL for the blog this post was created by. 64-pixels by 64-pixels.

{ReblogRootPortraitURL-96}Portrait photo URL for the blog this post was created by. 96-pixels by 96-pixels.

{ReblogRootPortraitURL-128}Portrait photo URL for the blog this post was created by. 128-pixels by 128-pixels.

{block:Reblogs}{/block:Reblogs}Rendering each reblog in the reblog trail for this post inside this block.

{block:IsActive} {/block:IsActive}Rendered when the blog that made this reblog trail item is active.

{block:IsDeactivated} {/block:IsDeactivated}Rendered when the blog that made this reblog trail item has been deactivated.

{Username}The name of the blog that made this reblog trail item.

{block:HasPermalink}{/block:HasPermalink}Rendered if a permalink to this post in the reblog trail exists.

{Permalink}Permalink to this post in the reblog trail.

{block:HasAvatar}{/block:HasAvatar}Rendered if the blog in the reblog trail item has a portrait photo.

{PortraitURL-16}Portrait photo URL for the blog in this reblog trail item. 16-pixels by 16-pixels.

{PortraitURL-24}Portrait photo URL for the blog in this reblog trail item. 24-pixels by 24-pixels.

{PortraitURL-30}Portrait photo URL for the blog in this reblog trail item. 30-pixels by 30-pixels.

{PortraitURL-40}Portrait photo URL for the blog in this reblog trail item. 40-pixels by 40-pixels.

{PortraitURL-48}Portrait photo URL for the blog in this reblog trail item. 48-pixels by 48-pixels.

{PortraitURL-64}Portrait photo URL for the blog in this reblog trail item. 64-pixels by 64-pixels.

{PortraitURL-96}Portrait photo URL for the blog in this reblog trail item. 96-pixels by 96-pixels.

{PortraitURL-128}Portrait photo URL the blog in this reblog trail item. 128-pixels by 128-pixels.

{block:isOriginalEntry} {/block:isOriginalEntry}Rendered when this reblog trail item is the original post content.

{Body}The HTML content of the reblog trail item.

A post can be either an original post (`{block:NotReblog} {/block:NotReblog}`) or a reblog (`{block:RebloggedFrom} {/block:RebloggedFrom}`) which may contain a reblog chain with other users' content added in their reblogs of the post. This chain of reblog content is what we call the **reblog trail**. Within the reblog trail, there can be multiple **reblog trail items** --- one item for each reblog with content. One such item is the original entry (`{block:isOriginalEntry} {/block:isOriginalEntry}`). 

The post content rendered by `{Body}` changes depending on the block context it is in. 

All NPF posts and legacy Text posts use `{Body}` to display the post content, other legacy post types use different variables. Please see the section for each post type below. 

Within the context of **reblogs**, `{Body}` renders the HTML content of a reblog trail item. 

Within the context of **original posts**, `{Body}` renders the post content for all NPF and legacy Text posts. Answer posts and some legacy post types use different variables to render **original post content** in reblog chains. `{Replies}` for Answer posts, `{Caption}` for legacy Photo and Photoset posts, `{Description}` for legacy Link, Video and Audio posts. 

Legacy Chat and Quote posts do not support the reblog variables listed in this section. 

#### Example
    
    {block:Text} <div class="post text"> {block:Title} <h3><a href="{Permalink}">{Title}</a></h3> {/block:Title} <!--Original Post--> {block:NotReblog} {Body} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} <div class="reblog-list"> {block:Reblogs} <div class="reblog-header"> {block:IsActive} <a href="{Permalink}">{Username}</a> {/block:IsActive} {block:IsDeactivated} <span>{Username}</span> {/block:IsDeactivated} </div> <div class="reblog-body">{Body}</div> {/block:Reblogs} </div> {/block:RebloggedFrom} </div> {/block:Text} 

### Neue Post Format

Nearly all Neue Post Format posts are rendered by legacy [Text post](https://www.tumblr.com/docs/en/custom_themes#text-posts) variables. There are two exceptions: 

1. **Answer posts** are rendered using the legacy [Answer post](https://www.tumblr.com/docs/en/custom_themes#answer-posts) variables. 
2. **Submission posts** still use legacy post types, and will only be rendered with the corresponding legacy post type. For example, a submitted photo post will be rendered as a legacy photo post. 

If you would like to have a little more control over the appearance of posts in your theme, you also have the option of using the `{NPF}` variable which will give you the Neue Post Format JSON representation of each post. You can use this to render your posts with JavaScript. You can find the full Neue Post Format specification on [GitHub](https://github.com/tumblr/docs/blob/master/npf-spec.md). 

### Legacy Text Posts

Also used to render the content of Neue Post Format posts.VariableDescription

{block:Title} {/block:Title}Rendered if there is a title for this post.

{Title}The title of this post.

{Body}The content of this post.

Note that all NPF-created posts will appear to be Text posts to your theme; however, the `{NPF}` variable (defined in the Posts section above) is available for all posts.

### Legacy Photo PostsVariableDescription

{PhotoAlt}The HTML-safe version of the caption (if one exists) of this post.

{block:Caption} {/block:Caption}Rendered if there is a caption for this post.

{Caption}The caption for this post.

{block:LinkURL}Rendered if this photo has a click-through set.

{LinkURL}A click-through URL for this photo. 

Defaults to media permalink if one is not set.

{LinkOpenTag}An HTML open anchor-tag including the click-through URL if set. 

Example: `<a href="https://...">`

{LinkCloseTag}A closing anchor-tag output only if a click-through URL is set. 

Example: `</a>`

{PhotoURL-500}URL for the photo of this post. No wider than 500-pixels.

{PhotoWidth-500}Width for the 500px size photo.

{PhotoHeight-500}Height for the 500px size photo.

{PhotoURL-400}URL for the photo of this post. No wider than 400-pixels.

{PhotoWidth-400}Width for the 400px size photo.

{PhotoHeight-400}Height for the 400px size photo.

{PhotoURL-250}URL for the photo of this post. No wider than 250-pixels.

{PhotoWidth-250}Width for the 250px size photo.

{PhotoHeight-250}Height for the 250px size photo.

{PhotoURL-100}URL for the photo of this post. No wider than 100-pixels.

{PhotoWidth-100}Width for the 100px size photo.

{PhotoHeight-100}Height for the 100px size photo.

{PhotoURL-75sq}URL for a square version of the photo of this post. 75-pixels by 75-pixels.

{block:HighRes} {/block:HighRes}Rendered if there is a high-res or panorama photo for a post.

{PhotoURL-HighRes}URL for the high-res or panorama sized photo of this post. No wider than 1280px or 2560px respectively. 

Use `{PhotoURL-1280}`, `{PhotoWidth-1280}`, and `{PhotoHeight-1280}` to access the 1280 media directly.

{PhotoWidth-HighRes}Width for the high-res size photo.

{PhotoHeight-HighRes}Height for the high-res size photo.

{block:Exif} {/block:Exif}Rendered if this photo has Exif data.

{block:Camera}  
{Camera}  
{/block:Camera}Rendered if this photo's Exif data contains camera info.

{block:Aperture}  
{Aperture}  
{/block:Aperture}Rendered if this photo's Exif data contains aperture info.

{block:Exposure}  
{Exposure}  
{/block:Exposure}Rendered if this photo's Exif data contains exposure info.

{block:FocalLength}  
{FocalLength}  
{/block:FocalLength}Rendered if this photo's Exif data contains focal length.

#### Example
    
    {Block:Photo}{LinkOpenTag} <img src="{PhotoURL-500}" alt="{PhotoAlt}"/>{LinkCloseTag}{block:HighRes} <a href="{PhotoURL-HighRes}">View in High-Res</a>{/block:HighRes}{block:Exif} <ul>{block:Camera} <li>Camera: {Camera}</li>{/block:Camera}{block:Aperture} <li>Aperture: {Aperture}</li>{/block:Aperture}{block:Exposure} <li>Exposure: {Exposure}</li>{/block:Exposure}{block:FocalLength} <li>Focal Length: {FocalLength}</li>{/block:FocalLength} </ul>{/block:Exif} <!--Original Post--> {block:NotReblog} {Caption} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} ... {/block:RebloggedFrom} {/Block:Photo} 

### Legacy Panorama Posts

The template tags defined for `{block:Photo}` are also available to `{block:Panorama}`, with the following additions: VariableDescription

{LinkOpenTag}An HTML open anchor-tag with Javascript to activate the Panorama lightbox.

{LinkCloseTag}A closing anchor-tag.

{PhotoURL-Panorama}URL for the panorama photo of this post. 

These images can be very big. (2560+ pixels wide)

{PhotoWidth-Panorama}Width for the panorama size photo.

{PhotoHeight-Panorama}Height for the panorama size photo.

### Legacy Photoset PostsVariableDescription

{block:Caption} {/block:Caption}Rendered if there is a caption for this post.

{Caption}The caption for this post.

{Photoset}Embed code for a responsive Photoset that shrinks to fit the container (max. 700-pixels wide).

{Photoset-700}Embed code for a 700-pixel wide photoset.

{Photoset-500}Embed code for a 500-pixel wide photoset.

{Photoset-400}Embed code for a 400-pixel wide photoset.

{Photoset-250}Embed code for a 250-pixel wide photoset.

{PhotoCount}The number of photos in the Photoset.

{PhotosetLayout}An integer representation of the Photoset layout.

{JSPhotosetLayout}JavaScript array of the Photoset column counts.

{block:Photos} {/block:Photos}Rendered for each of the Photoset photos. Each contains the same variables as {block:Photo}

#### Example
    
    {Block:Photoset} {Photoset} <!--Original Post--> {block:NotReblog} {Caption} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} ... {/block:RebloggedFrom} {/Block:Photoset} 

### Legacy Quote PostsVariableDescription

{Quote}The content of this post.

{block:Source} {/block:Source}Rendered if there is a source for this post.

{Source}The source for this post. 

May contain HTML

{Length}"short", "medium", or "long", depending on the length of the quote.

#### Example
    
    {block:Quote} "{Quote}" {block:Source} <div class="source">{Source}</div> {/block:Source} {/block:Quote} 

### Legacy Link PostsVariableDescription

{URL}The URL of this post.

{Name}The name of this post. Defaults to the URL if no name is entered.

{Target}Should be included inside the A-tags of Link posts. Output `target="_blank"` if you've enabled "Open links in new window".

{block:Host} {/block:Host}Rendered if there is a host for this post (if both URL and name exists).

{Host}The host name of the URL, sans 'www'. For example `tumblr.com`

{block:Thumbnail} {/block:Thumbnail}Rendered if there is an image thumbnail for the post.

{Thumbnail}Link thumbnail URL.

{Thumbnail-HighRes}Link high-res thumbnail URL.

{block:Description} {/block:Description}Rendered if there is a description for this post.

{Description}The description for this post.

{block:Author} {/block:Author}Rendered if the post includes an author.

{Author}The linked author's name.

{block:Excerpt} {/block:Excerpt}Rendered if the post includes an excerpt.

{Excerpt}The excerpt for this post.

#### Example
    
    {block:Link} <a href="{URL}" class="link" {Target}>{Name}</a> <!--Original Post--> {block:NotReblog} {Description} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} ... {/block:RebloggedFrom} {/block:Link} 

### Legacy Chat PostsVariableDescription

{block:Title} {/block:Title}Rendered if there is a title for this post.

{Title}The title of this post.

{block:Lines} {/block:Lines}Rendered for each line of this post.

{block:Label} {/block:Label}Rendered if a label was extracted for the current line of this post.

{Label}The label (if one was extracted) for the current line of this post.

{Name}The username (if one was extracted) for the current line of this post.

{Line}The current line of this post.

{UserNumber}A unique identifying integer representing the user of the current line of this post.

{Alt}"odd" or "even" for each line of this post.

#### Example
    
    {block:Chat} {block:Title} <h3><a href="{Permalink}">{Title}</a></h3> {/block:Title} <ul class="chat"> {block:Lines} <li class="{Alt} user_{UserNumber}"> {block:Label} <span class="label">{Label}</span> {/block:Label} {Line} </li> {/block:Lines} </ul> {/block:Chat} 

### Legacy Audio PostsVariableDescription

{block:Caption} {/block:Caption}Rendered if there is a caption for this post.

{Caption}The caption for this post.

{block:AudioEmbed} {/block:AudioEmbed}Rendered if an embedded audio player is available.

{AudioEmbed}Embed-code for the content of this post. Defaults to 500-pixels wide.

{AudioEmbed-250}Embed-code for the content of this post. 250-pixels wide.

{AudioEmbed-400}Embed-code for the content of this post. 400-pixels wide.

{AudioEmbed-500}Embed-code for the content of this post. 500-pixels wide.

{AudioEmbed-640}Embed-code for the content of this post. 640-pixels wide.

{block:AudioPlayer} {/block:AudioPlayer}Rendered if a native audio player is available

{AudioPlayer}Default audio player.

{RawAudioURL}URL for this post's audio file. 

[iPhone Themes](https://www.tumblr.com/docs/en/custom_themes#iphone-themes) only.

{block:PlayCount} {/block:PlayCount}Rendered if there is a play count for the audio.

{PlayCount}The number of times this post has been played.

{FormattedPlayCount}The number of times this post has been played, formatted with commas. 

e.g., `"12,309"`

{PlayCountWithLabel}The number of times this post has been played, formatted with commas and pluralized label 

e.g., `"12,309 plays"`

{block:ExternalAudio} {/block:ExternalAudio}Rendered if this post uses an externally hosted MP3\. 

Useful for adding a "Download" link

{ExternalAudioURL} The external MP3 URL, if this post uses an externally hosted MP3\. 

{block:AlbumArt}  
{AlbumArtURL}  
{/block:AlbumArt}Rendered if this audio file's ID3 info contains album art.

{block:Artist}  
{Artist}  
{/block:Artist}Rendered if this audio file's ID3 info contains the artist name.

{block:Album}  
{Album}  
{/block:Album}Rendered if this audio file's ID3 info contains the album title.

{block:TrackName}  
{TrackName}  
{/block:TrackName}Rendered if this audio file's ID3 info contains the track name.

#### Example
    
    {block:Audio} {block:AudioPlayer} <div class="audio_player"> {block:AlbumArt} <img src="{AlbumArtURL}"> {/block:AlbumArt} {AudioPlayer} </div> {/block:AudioPlayer} <div class="audio_info"> <ul> <li>Name: {block:TrackName}{TrackName}{/block:TrackName}</li> <li>Artist: {block:Artist}{Artist}{/block:Artist}</li> <li>Album: {block:Album}{Album}{/block:Album}</li> </ul> </div> <!--Original Post--> {block:NotReblog} {Description} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} ... {/block:RebloggedFrom} {/block:Audio} 

### Legacy Video PostsVariableDescription

{block:Caption} {/block:Caption}Rendered if there is a caption for this post.

{Caption}The caption for this post.

{Video-700}Embed-code for the content of this post. 700-pixels wide.

{Video-500}Embed-code for the content of this post. 500-pixels wide.

{Video-400}Embed-code for the content of this post. 400-pixels wide.

{Video-250}Embed-code for the content of this post. 250-pixels wide.

{VideoEmbed-700}Same as {Video-700}, but removes the lightbox effect from directly uploaded video. 700-pixels wide.

{VideoEmbed-500}Same as {Video-500}, but removes the lightbox effect from directly uploaded video. 500-pixels wide.

{VideoEmbed-400}Same as {Video-400}, but removes the lightbox effect from directly uploaded video. 400-pixels wide.

{VideoEmbed-250}Same as {Video-250}, but removes the lightbox effect from directly uploaded video. 250-pixels wide.

{PlayCount}The number of times this post has been played.

{FormattedPlayCount}The number of times this post has been played, formatted with commas. 

e.g., `"12,309"`

{PlayCountWithLabel}The number of times this post has been played, formatted with commas and pluralized label 

e.g., `"12,309 plays"`

{block:VideoThumbnail}  
{VideoThumbnailURL}  
{/block:VideoThumbnail}Rendered if there is a video thumbnail available.

{block:VideoThumbnails}  
{VideoThumbnailURL}  
{/block:VideoThumbnails}Rendered for each video thumbnail when there are multiple.

#### Example
    
    {block:Video} <div class="post video"> {Video-700} <!--Original Post--> {block:NotReblog} {Description} {/block:NotReblog} <!--Post is a reblog--> {block:RebloggedFrom} ... {/block:RebloggedFrom} </div> {/block:Video} 

### Legacy Answer Posts

Also used to render the content of Neue Post Format answer posts.VariableDescription

{Question}The question for this post. 

May contain heavily filtered HTML

{Answer}The answer for this post. 

May contain HTML

{Asker}Simple HTML text link with the asker's username and URL, or the plain text string "Anonymous".

{AskerPortraitURL-16}Portrait photo URL for the asker. 16-pixels by 16-pixels.

{AskerPortraitURL-24}Portrait photo URL for the asker. 24-pixels by 24-pixels.

{AskerPortraitURL-30}Portrait photo URL for the asker. 30-pixels by 30-pixels.

{AskerPortraitURL-40}Portrait photo URL for the asker. 40-pixels by 40-pixels.

{AskerPortraitURL-48}Portrait photo URL for the asker. 48-pixels by 48-pixels.

{AskerPortraitURL-64}Portrait photo URL for the asker. 64-pixels by 64-pixels.

{AskerPortraitURL-96}Portrait photo URL for the asker. 96-pixels by 96-pixels.

{AskerPortraitURL-128}Portrait photo URL for the asker. 128-pixels by 128-pixels.

{block:Answerer}{/block:Answerer}Rendered if post contains a reblogged answer.

{Answerer}Simple HTML text link with the reblogged answerer's username and URL. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.

{AnswererPortraitURL-16}Portrait photo URL for the reblogged answerer. 16-pixels by 16-pixels. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.')

{AnswererPortraitURL-24}Portrait photo URL for the reblogged answerer. 24-pixels by 24-pixels. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.

{AnswererPortraitURL-30}Portrait photo URL for the reblogged answerer. 30-pixels by 30-pixels. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.

{AnswererPortraitURL-40}Portrait photo URL for the reblogged answerer. 40-pixels by 40-pixels. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.

{AnswererPortraitURL-48}Portrait photo URL for the reblogged answerer. 48-pixels by 48-pixels. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.

{AnswererPortraitURL-64}Portrait photo URL for the reblogged answerer. 64-pixels by 64-pixels. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.

{AnswererPortraitURL-96}Portrait photo URL for the reblogged answerer. 96-pixels by 96-pixels. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.

{AnswererPortraitURL-128}Portrait photo URL for the reblogged answerer. 128-pixels by 128-pixels. 

Only exists within {block:Answerer}{/block:Answerer} and if post has been reblogged.

{Replies}Reblog chain. If not a reblog {Replies} is an alias for {Answer}

#### Example
    
    {block:Answer} <div class="question"> <div class="asker">{Asker}</div> <div class="asker-question">{Question}</div> <img class="asker-avatar" src="{AskerPortraitURL-96}" alt=""> </div> {block:Answerer} <div class="answer"> <div class="answerer">{Answerer}</div> <div class="answerer-answer">{Answer}</div> <img class="answerer-avatar" src="{AnswererPortraitURL-96}" alt=""> </div> {/block:Answerer} {block:NotReblog} {Replies} {/block:NotReblog} {block:RebloggedFrom} ... {/block:RebloggedFrom} {/block:Answer} 

### DatesVariableDescription

{block:Date} {/block:Date}Rendered for all posts. 

Always wrap dates in this block so they will be properly hidden on non-post pages.

{block:NewDayDate} {/block:NewDayDate}Rendered for posts that are the first to be listed for a given day.

{block:SameDayDate} {/block:SameDayDate}Rendered for subsequent posts listed for a given day.

{DayOfMonth}"1" to "31"

{DayOfMonthWithZero}"01" to "31"

{DayOfWeek}"Monday" through "Sunday"

{ShortDayOfWeek}"Mon" through "Sun"

{DayOfWeekNumber}"1" through "7"

{DayOfMonthSuffix}"st", "nd", "rd", "th"

{DayOfYear}"1" through "365"

{WeekOfYear}"1" through "52"

{Month}"January" through "December"

{ShortMonth}"Jan" through "Dec"

{MonthNumber}"1" through "12"

{MonthNumberWithZero}"01" through "12"

{Year}"2007"

{ShortYear}"07"

{AmPm}"am" or "pm"

{CapitalAmPm}"AM" or "PM"

{12Hour}"1" through "12"

{24Hour}"0" through "23"

{12HourWithZero}"01" through "12"

{24HourWithZero}"00" through "23"

{Minutes}"0" through "59"

{Seconds}"0" through "59"

{Beats}"0" through "999"

{Timestamp}"1172705619"

{TimeAgo}A contextual time. 

e.g., "1 minute ago", "2 hours ago", "3 weeks ago", etc.

### NotesVariableDescription

{block:PostNotes} {/block:PostNotes}Rendered on permalink pages if this post has notes.

{PostNotes}Standard HTML output of this post's notes. Only rendered on permalink pages.

{PostNotes-16}Standard HTML output of this post's notes with 16x16 sized avatars. Only rendered on permalink pages.

{PostNotes-64}Standard HTML output of this post's notes with 64x64 sized avatars. Only rendered on permalink pages.

{block:NoteCount} {/block:NoteCount} Rendered if this post has notes. 

Always wrap note counts in this block so they will be properly hidden on non-post pages.

{NoteCount}The number of this post's notes.

{NoteCountWithLabel}The number of this post's notes with pluralized label. 

e.g., "24 notes"

#### Example
    
    <html> <head> <style type="text/css"> ol.notes { padding: 0px; margin: 25px 0px; list-style-type: none; border-bottom: solid 1px #ccc; } ol.notes li.note { border-top: solid 1px #ccc; padding: 10px; } ol.notes li.note img.avatar { vertical-align: -4px; margin-right: 10px; width: 16px; height: 16px; } ol.notes li.note span.action { font-weight: bold; } ol.notes li.note .answer_content { font-weight: normal; } ol.notes li.note blockquote { border-color: #eee; padding: 4px 10px; margin: 10px 0px 0px 25px; } ol.notes li.note blockquote a { text-decoration: none; } </style> </head> <body> **{block:Posts}** ... **{PostNotes}****{/block:Posts}** </body> </html>

Notes are paginated with AJAX. If your theme needs to manipulate the Notes markup or DOM nodes, you can add a Javascript callback that fires when a new page of Notes is loaded or inserted:VariableDescription

tumblrNotesLoaded(notes\_html)If this Javascript function is defined, it will be triggered when a new page of Notes is loaded and ready to be inserted. If this function returns `false`, it will block the Notes from being inserted.

tumblrNotesInserted()If this Javascript function is defined, it will be triggered after a new page of Notes has been inserted into the DOM.

### TagsVariableDescription

{block:HasTags} {/block:HasTags}Rendered inside `{block:Posts}` if post has tags.

{block:Tags} {/block:Tags}Rendered for each of a post's tags.

{Tag}The name of this tag.

{URLSafeTag}A URL safe version of this tag.

{TagURL}The tag page URL with other posts that share this tag.

{TagURLChrono}The tag page URL with other posts that share this tag in chronological order.

#### Example
    
    <html> <body> **{block:Posts}** <div class="post"> **{block:Text}**...**{/block:Text}****{block:Photo}**...**{/block:Photo}** ... **{block:HasTags}** <ul class="tags"> **{block:Tags}** <li> <a href="**{TagURL}**">**{Tag}**</a> </li> **{/block:Tags}** </ul> **{/block:HasTags}** </div> **{/block:Posts}** </body> </html>

### Content SourcesVariableDescription

{block:ContentSource} {/block:ContentSource}Rendered if a source is specified for a post's content.

{SourceURL}URL of the attributed source.

{block:SourceLogo} {/block:SourceLogo}Rendered if a logo exists for the content source.

{BlackLogoURL}URL of the source's logo.

{LogoWidth}Width of the source's logo.

{LogoHeight}Height of the source's logo.

{SourceTitle}Title of the content source.

{block:NoSourceLogo} {/block:NoSourceLogo}Rendered if no source logo exists.

#### Example
    
    **{block:ContentSource}** <a href="**{SourceURL}**">**{lang:Source}**: **{block:SourceLogo}** <img src="**{BlackLogoURL}**" width="**{LogoWidth}**" height="**{LogoHeight}**" alt="**{SourceTitle}**" />**{/block:SourceLogo}****{block:NoSourceLogo}****{SourceTitle}****{/block:NoSourceLogo}** </a>**{/block:ContentSource}**

### SubmissionsVariableDescription

{block:Submission} {/block:Submission}Rendered if a post is a submission.

{Submitter}The name of the submitting blog.

{SubmitterURL}URL to submitter's blog.

{SubmitterPortraitURL-16}Portrait photo URL for the submitter. 16-pixels by 16-pixels.

{SubmitterPortraitURL-24}Portrait photo URL for the submitter. 24-pixels by 24-pixels.

{SubmitterPortraitURL-30}Portrait photo URL for the submitter. 30-pixels by 30-pixels.

{SubmitterPortraitURL-40}Portrait photo URL for the submitter. 40-pixels by 40-pixels.

{SubmitterPortraitURL-48}Portrait photo URL for the submitter. 48-pixels by 48-pixels.

{SubmitterPortraitURL-64}Portrait photo URL for the submitter. 64-pixels by 64-pixels.

{SubmitterPortraitURL-96}Portrait photo URL for the submitter. 96-pixels by 96-pixels.

{SubmitterPortraitURL-128}Portrait photo URL for the submitter. 128-pixels by 128-pixels.

## Group Blogs

### Group MembersVariableDescription

{block:GroupMembers} {/block:GroupMembers}Rendered on additional public group blogs.

{block:GroupMember} {/block:GroupMember}Rendered for each additional public group blog member.

{GroupMemberName}The username of the member's blog.

{GroupMemberTitle}The title of the member's blog.

{GroupMemberURL}The URL for the member's blog.

{GroupMemberPortraitURL-16}Portrait photo URL for the member. 16-pixels by 16-pixels.

{GroupMemberPortraitURL-24}Portrait photo URL for the member. 24-pixels by 24-pixels.

{GroupMemberPortraitURL-30}Portrait photo URL for the member. 30-pixels by 30-pixels.

{GroupMemberPortraitURL-40}Portrait photo URL for the member. 40-pixels by 40-pixels.

{GroupMemberPortraitURL-48}Portrait photo URL for the member. 48-pixels by 48-pixels.

{GroupMemberPortraitURL-64}Portrait photo URL for the member. 64-pixels by 64-pixels.

{GroupMemberPortraitURL-96}Portrait photo URL for the member. 96-pixels by 96-pixels.

{GroupMemberPortraitURL-128}Portrait photo URL for the member. 128-pixels by 128-pixels.

### Post AuthorsVariableDescription

{PostAuthorName}The username of the author of a post to an additional group blog.

{PostAuthorTitle}The title of the author's blog for a post to an additional group blog.

{PostAuthorURL}The blog URL for the author of a post to an additional group blog.

{PostAuthorPortraitURL-16}The portrait photo URL for the author of a post to an additional group blog. 16-pixels by 16-pixels.

{PostAuthorPortraitURL-24}The portrait photo URL for the author of a post to an additional group blog. 24-pixels by 24-pixels.

{PostAuthorPortraitURL-30}The portrait photo URL for the author of a post to an additional group blog. 30-pixels by 30-pixels.

{PostAuthorPortraitURL-40}The portrait photo URL for the author of a post to an additional group blog. 40-pixels by 40-pixels.

{PostAuthorPortraitURL-48}The portrait photo URL for the author of a post to an additional group blog. 48-pixels by 48-pixels.

{PostAuthorPortraitURL-64}The portrait photo URL for the author of a post to an additional group blog. 64-pixels by 64-pixels.

{PostAuthorPortraitURL-96}The portrait photo URL for the author of a post to an additional group blog. 96-pixels by 96-pixels.

{PostAuthorPortraitURL-128}The portrait photo URL for the author of a post to an additional group blog. 128-pixels by 128-pixels.

## Day Pages

Tumblr blogs can display posts from a given day using a URL like `https://david.tumblr.com/day/2007/04/29/` . By including the following markup, these pages can include pagination for the previous and next days with posts.VariableDescription

{block:DayPage} {/block:DayPage}Rendered on day pages.

{block:DayPagination} {/block:DayPagination}Rendered if there is a "previous" or "next" day page.

{block:PreviousDayPage} {/block:PreviousDayPage}Rendered if there is a "previous" day page to navigate to.

{block:NextDayPage} {/block:NextDayPage} Rendered if there is a "next" day page to navigate to. 

{PreviousDayPage}URL for the "previous" day page.

{NextDayPage}URL for the "next" day page.

#### Example
    
    <html> <body> <h1>**{Title}**</h1> **{block:DayPage}** <h2>**{Month}** **{DayOfMonth}**, **{Year}**</h2> **{/block:DayPage}** <ol id="posts"> **{block:Posts}** ... **{/block:Posts}** </ol> <div id="footer"> **{block:Pagination}****{block:PreviousPage}** <a href="**{PreviousPage}**">&#171; Previous</a> **{/block:PreviousPage}****{block:NextPage}** <a href="**{NextPage}**">Next &#187;</a> **{/block:NextPage}****{/block:Pagination}****{block:DayPagination}****{block:PreviousDayPage}** <a href="**{PreviousDayPage}**"> &#171; **{ShortMonth}** **{DayOfMonth}** </a> **{/block:PreviousDayPage}****{block:NextDayPage}** <a href="**{NextDayPage}**"> **{ShortMonth}** **{DayOfMonth}** &#187; </a> **{/block:NextDayPage}****{/block:DayPagination}** </div> </body> </html>

## Tag PagesVariableDescription

{block:TagPage} {/block:TagPage}Rendered on tag pages.

{Tag}The name of this tag.

{URLSafeTag}A URL safe version of this tag.

{TagURL}The tag page URL with other posts that share this tag.

{TagURLChrono}The tag page URL with other posts that share this tag in chronological order.

#### Example
    
    <html> <body> **{block:TagPage}** <h2>Posts tagged "**{Tag}**"</h2> **{/block:TagPage}****{block:Posts}** ... **{/block:Posts}** </body> </html>

## Localization

Localized theme strings allow your theme to appear in every language Tumblr supports. Simply replace any words or phrases in your theme with the appropriate variables. The full text will be output in the language designated in the blog's settings. [**Check out the strings →**](https://www.tumblr.com/docs/localizing_themes)

## SearchVariableDescription

{SearchQuery}The current search query.

{URLSafeSearchQuery}A URL-safe version of the current search query for use in links and Javascript.

{block:SearchPage}Rendered on search pages.

{SearchResultCount}The number of results returned for the current search query.

{block:NoSearchResults}Rendered if no search results were returned for the current search query.

{block:HideFromSearchEnabled} {/block:HideFromSearchEnabled}Rendered if the blog has chosen not to be indexed by search.

#### Example
    
    <form action="/search" method="get"> <input type="text" name="q" value="**{SearchQuery}**"/> <input type="submit" value="Search"/> </form>

## Featured TagsVariableDescription

{block:HasFeaturedTags} {/block:HasFeaturedTags}Rendered if the blog has any featured tags.

{block:FeaturedTags} {/block:FeaturedTags}Rendered for each of the blog's featured tags.

{Tag}The name of this tag.

{URLSafeTag}A URL safe version of this tag.

{TagURL}The tag page URL with other posts that share this tag.

{TagURLChrono}The tag page URL with other posts that share this tag in chronological order.

#### Example
    
    <html> <body> ... **{block:HasFeaturedTags}** <ul class="featured-tags"> **{block:FeaturedTags}** <li> <a href="**{TagURL}**">**{Tag}**</a> </li> **{/block:FeaturedTags}** </ul> **{/block:HasFeaturedTags}** ... </body> </html>

## FollowingVariableDescription

{block:Following} {/block:Following}Rendered if you're following other blogs.

{block:Followed} {/block:Followed}Rendered for each blog you're following.

{FollowedName}The username of the blog you're following.

{FollowedTitle}The title of the blog you're following.

{FollowedURL}The URL for the blog you're following.

{FollowedPortraitURL-16}Portrait photo URL for the blog you're following. 16-pixels by 16-pixels.

{FollowedPortraitURL-24}Portrait photo URL for the blog you're following. 24-pixels by 24-pixels.

{FollowedPortraitURL-30}Portrait photo URL for the blog you're following. 30-pixels by 30-pixels.

{FollowedPortraitURL-40}Portrait photo URL for the blog you're following. 40-pixels by 40-pixels.

{FollowedPortraitURL-48}Portrait photo URL for the blog you're following. 48-pixels by 48-pixels.

{FollowedPortraitURL-64}Portrait photo URL for the blog you're following. 64-pixels by 64-pixels.

{FollowedPortraitURL-96}Portrait photo URL for the blog you're following. 96-pixels by 96-pixels.

{FollowedPortraitURL-128}Portrait photo URL for the blog you're following. 128-pixels by 128-pixels.

#### Example
    
    **{block:Following}** Blogs I follow: <ul>**{block:Followed}** <li> <img src="**{FollowedPortraitURL-48}**"/> <a href="**{FollowedURL}**">**{FollowedName}**</a> </li>**{/block:Followed}** </ul>**{/block:Following}**

## LikesVariableDescription

{block:Likes} {/block:Likes}Rendered if you are [sharing your likes](https://www.tumblr.com/settings).

{block:NoLikes} {/block:NoLikes}Rendered if a blog has no likes. Please note that only primary blogs can have likes.

{Likes}Standard HTML output of your likes.

{Likes limit="5"}Standard HTML output of your last 5 likes. 

Maximum: 10

{Likes width="200"}Standard HTML output of your likes with Audio and Video players scaled to 200-pixels wide. 

Scale images with CSS max-width or similar.

{Likes summarize="100"}Standard HTML output of your likes with text summarized to 100-characters. 

Maximum: 250

#### Example
    
    <html> <head> <style type="text/css"> ul#likes { list-style-type: none; margin: 0 0 0 0; padding: 0 0 0 0; } li.like_post { /* _Should match the width specified in the Likes tag_ */ width: 150px; padding: 0 40px 0 0; float: left; } li.like_post img { max-width: 100%; } li.like_post blockquote { margin: 0; padding: 0 0 0 10px; border-left: 1px solid #eee; } li.like_post ol, li.like_post ul { margin: 0 0 0 15px; padding: 0; } li.like_post .like_link a { font-weight: bold; } li.like_post .like_title { font-weight: bold; } li.like_post .post_info_bottom { margin: 10px 0 0 0; display: block !important; } </style> </head> <body> ... **{block:Likes}** <div id="likes_container"> <h2>Stuff I like</h2> **{Likes limit="5" summarize="100" width="150"}** <a href="https://www.tumblr.com/liked/by/**{Name}**"> See more stuff I like </a> </div> **{/block:Likes}** </body> </html>

## Like and Reblog buttons

### Like ButtonVariableDescription

{LikeButton}Default Like button.

{LikeButton color="grey"}Like button color. 

Grey, White, or Black. Like button will always be red if visitor has liked the post.

{LikeButton size="20"}Like button size. 

Maximum: 100

### Reblog ButtonVariableDescription

{ReblogButton}Default Reblog button.

{ReblogButton color="grey"}Reblog button color. 

Grey, White, or Black.

{ReblogButton size="20"}Reblog button size. 

Maximum: 100

#### Example
    
    <html> <head> <style type="text/css"> .like_and_reblog_buttons { border: 1px solid #e8e8e8; border-radius: 3px; list-style: none; } .like_and_reblog_buttons li { float: left; margin: 0; padding: 7px 15px; height: 20px; } .like_and_reblog_buttons li:first-child { border-right: 1px solid #e8e8e8; } </style> </head> <body> ... **{block:Posts}** ... <ul class="like_and_reblog_buttons"> <li>**{ReblogButton}**</li> <li>**{LikeButton}**</li> </ul> **{/block:Posts}** ... </body> </html>

If your theme uses infinite scrolling or some other form of AJAX pagination, you must request the like status of the new posts once the page is loaded or inserted:FunctionDescription

Tumblr.LikeButton.get\_status\_by\_page(n)Call this function after requesting a new page of Posts. Takes the page number that was just loaded as an integer.

Tumblr.LikeButton.get\_status\_by\_post\_ids(\[n,n,n\])Request Like status for individual posts. Takes an array of post IDs.

## Related PostsVariableDescription

{block:RelatedPosts} {/block:RelatedPosts}Rendered on permalink pages. Shows related posts using post type, content, and tags as reference. Follows the same format as the [Posts](https://www.tumblr.com/docs/en/custom_themes#posts) block.

#### Example
    
    <html> <body> **{block:IfRelatedPosts}****{block:RelatedPosts}** <h2>Related Posts</h2> **{block:Posts}** ... **{/block:Posts}****{/block:RelatedPosts}****{/block:IfRelatedPosts}** </body> </html>

## Theme Options

### Enabling Custom Colors

By including special meta-color tags in your theme, users can easily tweak those colors using the [Customize](https://www.tumblr.com/customize) page.

You can also specify `{BackgroundColor}`, `{TitleColor}`, or `{AccentColor}` as defaults to inherit values from the [global appearance](https://www.tumblr.com/docs/en/custom_themes#global_appearance) parameters unless the user chooses another color manually.

#### Example
    
    <html> <head> <!-- DEFAULT COLORS --> <meta name="color:Background" content="#eee"/> <meta name="color:Content Background" content="#fff"/> <meta name="color:Heading text" content="{TitleColor}"/> <meta name="color:Text" content="#000"/> <style type="text/css"> #title { color: **{color:Heading text}**; } #content { background-color: **{color:Content Background}**; color: **{color:Text}**; } </style> </head> <body bgcolor="**{color:Background}**"> <h1 id="title">Title</h1> <div id="content"> ... </div> </body> </html>

### Enabling Custom Fonts

By including special meta-font tags in your theme, users can easily change those fonts using the [Customize](https://www.tumblr.com/customize) page.

You can also specify `{TitleFont}` as the default to inherit the value from the "Title font" [global appearance](https://www.tumblr.com/docs/en/custom_themes#global_appearance) parameter unless the user chooses a different font manually.

#### Example
    
    <html> <head> <!-- DEFAULT FONTS --> <meta name="font:Title" content="Helvetica Neue"/> <meta name="font:Body" content="Arial, Helvetica, sans-serif"/> <style type="text/css"> h1 { font: 30px **{font:Title}**; } #content { font: 12px **{font:Body}**; } </style> </head> ... </html>

### Enabling Booleans

By including special meta-if tags in your theme, users can easily toggle options you define. This is useful for showing or hiding different widgets or design elements.

#### Example
    
    <html> <head> <!-- DEFAULTS --> <meta name="if:Show people I follow" content="0"/> <meta name="if:Reverse pagination" content="1"/> </head> <body> **{block:IfNotReversePagination}** <a href="...">Previous</a> <a href="...">Next</a> **{/block:IfNotReversePagination}****{block:IfReversePagination}** <a href="...">Next</a> <a href="...">Previous</a> **{/block:IfReversePagination}****{block:IfShowPeopleIFollow}** <div id="following">...</div> **{/block:IfShowPeopleIFollow}** </body> </html>

### Enabling drop-down lists

By including special meta-select tags in your theme, you can give users several options for a particular design element.

#### Example
    
    <html> <head> <!-- DEFAULTS --> <meta name="select:Layout" content="regular" title="Regular"> <meta name="select:Layout" content="narrow" title="Narrow"> <meta name="select:Layout" content="grid" title="Grid"> </head> <body> <div class="content **{select:Layout}**"> ... </div> </body> </html>

### Enabling Custom Text

By including special meta-text tags in your theme, users can easily configure text variables you define. This is useful for adjusting text or configuring widgets that require information from the user.

#### Example
    
    <html> <head> <!-- DEFAULT TEXT --> <meta name="text:Flickr Username" content=""/> </head> <body> **{block:IfFlickrUsername}** <div id="flickr_widget"> <script type="text/javascript" src="https://flickr.com/widget?user=**{text:Flickr Username}**"> </script> </div> **{/block:IfFlickrUsername}** </body> </html>

### Enabling Custom Images

By including special meta-image tags in your theme, users can easily use custom images without editing your theme. Image variables (e.g., `{image:Logo}` ) will return a 1-pixel transparent square if no image is set.

You can also specify `{HeaderImage}` as the default to inherit the value from the "Header image" [global appearance](https://www.tumblr.com/docs/en/custom_themes#global_appearance) parameter until the user uploads a different image.

#### Example
    
    <html> <head> <!-- DEFAULT IMAGE --> <meta name="image:Background" content="https://static.tumblr.com/..."/> <meta name="image:Header" content="**{HeaderImage}**"/> <style type="text/css"> body { background: #2D567C url('**{image:Background}**'); } </style> </head> <body> **{block:IfHeaderImage}**<img src="**{image:Header}**"/>**{/block:IfHeaderImage}**  **{block:IfNotHeaderImage}**<h1>**{Title}**</h1>**{/block:IfNotHeaderImage}** </body> </html>

### Enabling Custom CSS

By including the `{CustomCSS}` tag at the bottom of your theme's CSS style block, users you share your theme with will be able to tweak the appearance of your theme without editing its markup.

#### Example
    
    <html> <head> <style type="text/css"> #content { background-color: #fff; color: #000; } **{CustomCSS}** </style> </head> <body> <div id="content"> ... </div> </body> </html>

## Theme Assets

You can upload, manage and insert theme assets in the [Customizer](https://help.tumblr.com/hc/articles/230778847-Custom-HTML).

Any assets used in your theme must be served over HTTPS.

## Mobile Themes

By default, Tumblr blogs display the default mobile theme on mobile devices, but you can change this in the [Customizer](https://help.tumblr.com/hc/articles/230778847-Custom-HTML).

## Variable Transformations

By prefixing variables with special transformation keywords, Tumblr will output variables in specialized formats --- useful when passing data to Javascript, etc. Tumblr currently supports five transformations:VariableDescription

PlaintextPrefix any theme variable with `Plaintext` to output the string with HTML-tags stripped and appropriate characters converted to HTML-entities so they're safe to include in HTML attributes, etc.

JavascriptPrefix any theme variable with `JS` to output a Javascript string (wrapped in quotes).

Javascript PlaintextPrefix any theme variable with `JSPlaintext` to output a Javascript string (wrapped in quotes) with HTML-tags stripped and appropriate characters converted to HTML-entities.

URLEncodedPrefix any theme variable with `URLEncoded` to output a URL encoded string.

RGBPrefix a color variable with `RGB` to convert the hex output to RGB.

#### Example
    
    <a href="**{URL}**" title="**{PlaintextName}**">**{Name}**</a> <script type="text/javascript"> var description = **{JSDescription}**; var description_text = **{JSPlaintextDescription}**; </script> <a href="http://digg.com/submit?url=**{URLEncodedPermalink}**">Digg this</a>

* **[(c) Tumblr, Inc.](https://www.tumblr.com/)**
* [Help](https://www.tumblr.com/help)
* [About](https://www.tumblr.com/about)
* [Apps](https://www.tumblr.com/apps)
* [Developers](https://www.tumblr.com/developers)
* [Themes](https://www.tumblr.com/themes/)
* [Jobs](https://www.tumblr.com/jobs)
* [Legal](https://www.tumblr.com/policy/terms-of-service)
* [Privacy ](https://www.tumblr.com/policy/privacy)