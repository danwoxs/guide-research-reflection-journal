

# CONTRIBUTING TO EXTERNAL COMMUNITY

  
## Introduction

I see a perfect opportunity to contribute on the Google Lighthouse an industry-standard tool by addressing Issue #15877. This issue concerns the lack of visual feedback, specifically the inability for a user to click on timeline images to open the full-size images.

  

My contribution will focus on enhancing this visual feedback by implementing a hover interaction to display the full image. This task is an excellent entry point for applying my front-end development skills in a production codebase, offering valuable practice in precise styling, interactive design, and contributing to the maintenance of a widely-used project.

  

My plan is to add a hover or focus interaction on the filmstrip thumbnails that displays the full-size screenshot as a positioned overlay. The implementation would:

  

\- Use CSS-driven scaling with smooth transitions

\- Support both hover and keyboard focus for accessibility

\- Handle edge-of-viewport positioning to prevent clipping

\- Work within the existing renderer patterns with no new dependencies

  
  

\## Understanding the Issue

  

Lighthouse's performance report includes a filmstrip timeline showing page load screenshots. Currently, these thumbnail images are static. Users can't click or hover to see a full-size version, which makes it hard to inspect visual details during the loading process. Issue #15877 requests that interaction.

  

## Approach Plan

  

A hover-based interaction to show the full image is a solid UX choice for this context; it's lightweight, doesn't require navigation, and fits the "inspection" mental model developers have when reviewing performance audits.

  

## Breakdown

  

The filmstrip component in Lighthouse's report renderer. The codebase lives under \`lighthouse-core/report/html/renderer/\` (or a similar path in the current repo structure). You'll want to find where the timeline thumbnails are rendered, likely in a component dealing with "filmstrip" or "screenshot" elements.

  

## Implementation considerations

The hover interaction itself is fairly straightforward, but doing it well in a production codebase means thinking about a few things. First, \*\*positioning logic\*\*  the enlarged image needs to appear in a sensible place relative to the thumbnail without overflowing the viewport, especially for thumbnails near screen edges. Second, \*\*accessibility\*\* hover alone isn't keyboard-accessible, so you'll want to consider focus-based triggering too (\`:focus\` alongside \`:hover\`, or a click-to-toggle fallback). Third, \*\*performance\*\* the full-size images are likely already in the report data, so you probably don't need to fetch anything, just display what's already there at a larger scale. And fourth, \*\*styling consistency\*\*  match the existing report's design language (shadows, borders, transitions, z-index layering).

  

## A reasonable implementation pattern:

  

Use a CSS-driven approach where hovering a thumbnail triggers a scaled-up overlay, positioned absolutely relative to the thumbnail container. Something like a tooltip-style popup with the full image. If the Lighthouse report renderer uses web components or a template system, you'll want to work within that pattern rather than introducing a new paradigm.

  

## Recommended Next Steps

  

Clone the repo and get the report rendering locally so you can test changes visually. Read through the existing filmstrip rendering code to understand the data flow, where do the screenshot images come from, how are they sized, what component owns them? 

  

## Challenges

  

The hardest part is \*\*viewport-aware positioning of the overlay\*\*.

  

Here's why it's deceptively tricky: the filmstrip is a horizontal row of thumbnails, and any of them could be near the edges of the viewport: left, right, top, or bottom depending on scroll position and screen size. When you show a full-size screenshot overlay, you need to figure out \*where\* to place it so it's actually visible.

  

This means you're dealing with several interacting constraints at once. You need to detect the thumbnail's position relative to the viewport (not just its parent container) using something like \`getBoundingClientRect()\`. Then you need to decide whether the overlay should appear above, below, left, or right of the thumbnail - and that decision changes depending on which edge is closest. You also have to account for varying screen sizes, since Lighthouse reports are viewed on everything from narrow laptop screens to wide monitors. And the filmstrip scrolls horizontally, so a thumbnail's viewport position changes dynamically.

  

A pure CSS approach (like \`transform: scale()\`) is simpler but breaks down at the edges, a scaled-up image anchored to a thumbnail on the far right will overflow off-screen. So you'll likely need some JavaScript to measure positions and adjust placement, which adds complexity and means you're mixing CSS transitions with JS-driven positioning logic.

  

On top of that, you have to keep this performance. Hover events fire rapidly, and calling layout-triggering APIs like \`getBoundingClientRect()\` on every hover can cause jank if you're not careful.

  

## Possible Solution

  

To start with the simplest version first a CSS \`transform: scale()\` centered on the thumbnail and note the edge-clipping limitation in your PR. That gives maintainers something concrete to review, and the positioning refinement can be iterated on. Trying to ship the perfect edge-aware solution on a first contribution adds risk without necessarily being what the maintainers want.