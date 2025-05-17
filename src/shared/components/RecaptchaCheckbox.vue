<template>
  <div ref="recaptchaContainer"></div>
</template>

<script>
export default {
  name: 'RecaptchaCheckbox',
  mounted() {
    const renderRecaptcha = () => {
      if (window.grecaptcha && window.grecaptcha.render) {
        window.onVerify = (token) => {
          this.$emit('verified', token);
        };
        window.onExpired = () => {
          this.$emit('expired');
        };

        window.grecaptcha.render(this.$refs.recaptchaContainer, {
          sitekey: '6LficTUrAAAAAJfjHo_RB4SHdj77995t-LkAM32s',
          callback: 'onVerify',
          'expired-callback': 'onExpired'
        });
      } else {
        setTimeout(renderRecaptcha, 300); // Espera y vuelve a intentar
      }
    };

    renderRecaptcha();
  }
};
</script>
