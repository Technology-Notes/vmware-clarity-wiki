The concept of virtual scrolling is to allow for an unlimited number of items to be inside of a fixed container, and as you scroll more items are added to the list to keep it growing. For performance reasons, the number of actual items rendered on the screen is limited to a smaller amount and the virtual scroller will create and destroy items as the user scrolls up and down to keep enough items in view but not many more.

It is considered good for performance because of the ability to show a lot of items in a nearly infinite list, but not actually render them all. It is commonly used in social media websites since the amount of content they have is essentially infinite, and always growing faster than you can consume it. In other applications, its often used in place of pagination or other patterns to navigate long lists.

***

# Status: ❌ Won't implement

Virtual scrolling (inside of Datagrid or other contexts) has a number of technical and usability issues.

## Usability issues

While virtual scrolling may be good for performance (though it adds complexity to the application), it can be frustrating for users who are scanning for an item. In social-media, you are just consuming casually the content but in a task-oriented setting you need to find an item or two, and endless scrolling often brings frustration to the user. 

Resource: https://www.nngroup.com/articles/infinite-scrolling/

### Technical issues

Firefox has an implementation of scroll-linked effects (which are means to handle scrolling behavior manually), and there is an asynchronous behavior to how it handles these events. This leads to lag, especially on content heavy websites, but even on any website there could be several frames of lag for the scrolling behavior. Here is a technical reason why scroll-linked effects should be avoided.

Resource: https://developer.mozilla.org/en-US/docs/Mozilla/Performance/Scroll-linked_effects

The ability to define and style scroll bars is also very limited and inconsistent across browsers, so it is essentially not something we can control in many browsers. Scroll bars are essential to giving scale of content and access for users to manage the scrolling without using a mouse wheel.

Resource: https://caniuse.com/#feat=css-scrollbar