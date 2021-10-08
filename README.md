# Callback vs Promise vs Async
Javscript Note

##  Callback
```javascript
getUser(1, (user) => {
    getBlogPosts(user.name, (blogposts) => {
        getComments(blogposts[0], (comments) => {
            console.log(user, blogposts[0], comments);
        })
    })
});
 
function getUser(id, callbackfunc) {
    setTimeout(() => {
        console.log('Getting the user from the database...');
        callbackfunc({
            id: id,
            name: 'Vegibit'
        });
    }, 1000);
}
 
function getBlogPosts(username, callbackfunc) {
    setTimeout(() => {
        console.log('Calling WordPress Rest API for posts');
        callbackfunc(['Post1', 'post2', 'post3']);
    }, 1000);
}
 
function getComments(post, callbackfunc) {
    setTimeout(() => {
        console.log('Calling WordPress Rest API for comments for ' + post);
        callbackfunc(['comments for ' + post]);
    }, 1000);
}
```
### Callback with name  

```javascript
getUser(1, getUserBlogPosts);
 
function getUser(id, callbackfunc) {
    setTimeout(() => {
        console.log('Getting the user from the database...');
        callbackfunc({
            id: id,
            name: 'Vegibit'
        });
    }, 1000);
}
 
function getUserBlogPosts(user) {
    getBlogPosts(user.name, getPosts);
}
 
function displayComments(comments) {
    console.log(comments);
}
 
function getPosts(blogposts) {
    getComments(blogposts[0], displayComments);
}
 
function getBlogPosts(username, callbackfunc) {
    setTimeout(() => {
        console.log('Calling WordPress Rest API for posts');
        callbackfunc(['Post1', 'post2', 'post3']);
    }, 1000);
}
 
function getComments(post, callbackfunc) {
    setTimeout(() => {
        console.log('Calling WordPress Rest API for comments for ' + post);
        callbackfunc(['comments for ' + post]);
    }, 1000);
}

```
## Promises

```javascript

// getUser(1, (user) => {
//     getBlogPosts(user.name, (blogposts) => {
//         getComments(blogposts[0], (comments) => {
//             console.log(user, blogposts[0], comments);
//         })
//     })
// });
 
getUser(1)
    .then(user => getBlogPosts(user.name))
    .then(blogposts => getComments(blogposts[0]))
    .then(comments => console.log(comments))
    .catch(err => console.log('Error: ', err.message));
 
function getUser(id) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            console.log('Getting the user from the database...');
            resolve({
                id: id,
                name: 'Vegibit'
            });
        }, 1000);
    });
}
```
