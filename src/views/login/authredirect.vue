<script>
export default {
  name: 'AuthRedirect',
  created() {
    const hash = window.location.hash.slice(1)
     window.opener.location.href = window.location.origin + '#/login?' + hash.split("?")[1]
    window.close()
  }
}
</script>
