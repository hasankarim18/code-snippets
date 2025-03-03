- html sample

```
 <button
            data-variant-id="{{ product.variants.first.id }}"
            data-product-card-id="{{product.id}}"
            class=" bg-violet-700 hover:bg-violet-900  text-white btn-full">Add to cart</button>
```

```
document.addEventListener('DOMContentLoaded', () => {
const productCardAddtoCart = () => {
const addToCartBtns = document.querySelectorAll('[data-variant-id]');

        addToCartBtns.forEach((btn) => {
            btn.addEventListener('click', async (e) => {
                const variantId = btn.getAttribute('data-variant-id');

                if (!variantId) {
                    alert('Error: Product variant ID is missing.');
                    console.error('Error: Variant ID is missing.');
                    return;
                }

                btn.disabled = true; // 🚀 Disable the button during API call
                btn.innerText = "Adding..."; // Optional: Change text to indicate action

                let formData = {
                    'items': [{
                        'id': parseInt(variantId, 10),
                        'quantity': 1
                    }]
                };

                try {
                    let response = await fetch(window.Shopify.routes.root + 'cart/add.js', {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify(formData)
                    });

                    let data = await response.json();

                    if (data.items && data.items.length > 0) {
                        alert('✅ Product added to cart successfully!');

                        // ✅ FIRE ANOTHER API CALL HERE AFTER SUCCESSFUL ADD-TO-CART
                        // Example:
                        // await fetch('YOUR_API_ENDPOINT_HERE', { method: 'POST', body: JSON.stringify(data) });

                        console.log('Added to cart:', data);
                    } else {
                        throw new Error('Failed to add product to cart.');
                    }
                } catch (error) {
                    alert('❌ Error adding product to cart. Please try again.');
                    console.error('Error:', error);
                } finally {
                    btn.disabled = false; // 🔄 Re-enable button after API call completion
                    btn.innerText = "Add to Cart"; // Restore button text
                }
            });
        });
    };

    productCardAddtoCart();

});


```
