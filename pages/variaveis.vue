<template>
  <div style="background-color: black;">
    <div style="display: flex; justify-content: center;">
      <div style="width: 50%; display: inline-block; border: 1px solid white; ">
        <div>
          <svg viewBox="0 0 24 24" aria-hidden="true" class="r-4qtqp9 r-yyyyoo r-dnmrzs r-bnwqim r-1plcrui r-lrvibr r-1nao33i r-rxcuwo r-1777fci r-m327ed r-494qqr"><g><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"></path></g></svg>
        </div>  
      </div>
      <div style="width: 50%; display: inline-block;position: relative;">
        <div style="position: absolute; left: 100px; top: 70px;">
          <v-row>
            <h1 style="font-size: 62px;">Acontecendo agora</h1>
          </v-row>
          <v-row>
            <h2 style="font-size: 30px; padding-top: 30px;">Inscreva-se hoje</h2>
          </v-row>
          <v-row>
            <v-btn
              rounded="xl"
              variant="text"
              class="text-none">
                <v-icon>
                  mdi-google
                </v-icon>
                Inscrever-se no Google
            </v-btn>
          </v-row>
          <v-row>
            <v-btn
              rounded="xl"
              variant="text"
              class="text-none">
                <v-icon>
                  mdi-apple
                </v-icon>
                Inscrever-se com Apple
            </v-btn>
          </v-row>
          <v-row>

          </v-row>
          <v-row>
            <v-btn
              rounded="xl"
              variant="text"
              class="text-none">
                Criar conta
            </v-btn>
          </v-row>
        </div>
      </div>
    </div>
    <div>
      <v-layout>
        <v-template>
          <v-footer class="bg-black">
            <v-row justify="center" no-gutters>
              <a
              v-for="link in links"
              :key="link"
              class="ml-2"
              :href="link.link"
              color="grey"
              style="font-size: 12px;"
              :class="visitade"
              >
              {{ link.nome }}
            </a>
          </v-row>
          </v-footer>
        </v-template>
      </v-layout>
    </div>
  </div>
</template>

<script>
  export default {
    data: () => ({
      links: [
        {
          nome: 'About',
          link: 'https://google.com'
        },
        {
          nome: 'Download the X app',
          link: 'https://google.com'
        },
        {
          nome: 'Help Center',
          link: 'https://google.com'
        },
        {
          nome: 'Terms of Service',
          link: 'https://google.com'
        },
        {
          nome: 'Privacy Policy',
          link: 'https://google.com'
        },
        {
          nome: 'Cookie Policy',
          link: 'https://google.com'
        },
        {
          nome: 'Accessibility',
          link: 'https://google.com'
        },
        {
          nome: 'Ads info',
          link: 'https://google.com'
        },
        {
          nome: 'Blog',
          link: 'https://google.com'
        },
        {
          nome: 'Careers',
          link: 'https://google.com'
        },
        {
          nome: 'Brand Resources',
          link: 'https://google.com'
        },
        {
          nome: 'Advertising',
          link: 'https://google.com'
        },
        {
          nome: 'Marketing',
          link: 'https://google.com'
        },
        {
          nome: 'Download the X app',
          link: 'https://google.com'
        },
        {
          nome: 'X for Business',
          link: 'https://google.com'
        },
        {
          nome: 'Developers',
          link: 'https://google.com'
        },
        {
          nome: 'Directory',
          link: 'https://google.com'
        },
        {
          nome: 'Settings',
          link: 'https://google.com'
        },
        {
          nome: '© 2024 X Corp.',
          link: 'https://google.com'
        },
      ],
    }),
  }
</script>

<style>
a:visited {
  text-decoration: none;
  color: grey;
}
</style>