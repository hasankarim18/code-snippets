# Title

### How to rotate a `+` icon 180 deg or any other

```
- const initializeRotateOnHover = () => {
  // Select all parent elements with the data-rotate-wrapper attribute
  const wrappers = document.querySelectorAll("[data-rotate-wrapper]");

  // Loop through each parent element
  wrappers.forEach((wrapper) => {
  // Find the child element with the data-rotate-180 attribute
  const child = wrapper.querySelector("[data-rotate-180]");

      // If the child exists, add event listeners to the parent
      if (child) {
        // Add event listener for mouseenter (hover on parent)
        wrapper.addEventListener("mouseenter", () => {
          child.style.transition = "transform 500ms ease";
          child.style.transform = "rotate(180deg)";
        });

        // Add event listener for mouseleave (hover off parent)
        wrapper.addEventListener("mouseleave", () => {
          child.style.transition = "transform 500ms ease";
          child.style.transform = "rotate(0deg)";
        });
      }

  });
  };

// Execute the function as soon as the page is loaded
window.addEventListener("DOMContentLoaded", initializeRotateOnHover);
```

⭐⭐ Run the above function

- parent attribute: `data-rotate-wrapper`
- child attribut: `data-rotate-180`

```
<div  data-rotate-wrapper >
    <button>
        <span data-rotate-180 >
            +
        </span>
    </button>
</div>
```

- when you will hover on the `data-roatate-wrapper` the child `data-rotate-180` will rotate 180 and vice versa
  `
