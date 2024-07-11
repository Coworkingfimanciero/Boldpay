Puedo cargar y guardar este código en Google colab para generar una url que haga las veces el botón: 

<script>
const initBoldCheckout = () => {
    if (document.querySelector('script[src="https://checkout.bold.co/library/boldPaymentButton.js"]')) {
        console.warn('Bold Checkout script is already loaded.');
        return;
    }

    var js;
    js = document.createElement('script');
    js.onload = () => {
        window.dispatchEvent(new Event('boldCheckoutLoaded'));
    };
    js.onerror = () => {
        window.dispatchEvent(new Event('boldCheckoutLoadFailed'));
    };
    js.src = 'https://checkout.bold.co/library/boldPaymentButton.js';
    document.head.appendChild(js);
};

initBoldCheckout();

// Event listener para cuando el script de Bold se haya cargado correctamente
window.addEventListener('boldCheckoutLoaded', () => {
    const checkout = new BoldCheckout({
        apiKey: 'l884Ny2fdD4uADNq00aWAXU2wo44kjyUPE2zlvRf838',
        merchantId: '9XW3IZZ86Z',
        integrationKey: 'l884Ny2fdD4uADNq00aWAXU2wo44kjyUPE2zlvRf838',
        currency: 'COP',
        reverseUrl: 'https://www.comerciolatam.online/junio2024#top',
        description: 'Depósito de fondos',
    });

    const customButton = document.getElementById('custom-button');
    const amountInput = document.getElementById('amount-input');

    if (customButton && amountInput) {
        customButton.addEventListener('click', () => {
            const amount = parseFloat(amountInput.value);
            if (isNaN(amount) || amount <= 0) {
                alert('Por favor ingrese un monto válido.');
                return;
            }
            checkout.open({
                amount: amount,
            });
        });
    } else {
        console.error('Custom button or amount input not found.');
    }
});

window.addEventListener('boldCheckoutLoadFailed', () => {
    console.error('Failed to load Bold Checkout script.');
});
</script>
