<script context="module">

  export const meta = {
      title: 'Button2',
      parameters: {
          sveltekit_experimental: {
              stores: {
                  page: {
                      url: {
                          searchParams: new URLSearchParams(),
                      },
                  },
              },
              navigation: {
                  invalidateAll: () => console.log(`invalidateAll called`),
                  beforeNavigate: () => console.log(`beforeNavigate called`),
                  afterNavigate: () => ({ foo: 'bar' }),
              },
          },
      },
  }
</script>


<script>
  import { Story } from '@storybook/addon-svelte-csf';
  
  import { z } from 'zod';
  import { superValidateSync } from 'sveltekit-superforms/client';
  import { superForm } from 'sveltekit-superforms/client';

  const testSchema = z.object({
          name: z.string().min(2),
      });
  const formValidated = superValidateSync({ name: 'ole' }, testSchema);

  /**
   * The following line breaks storybook with:
   * Cannot destructure property 'story' of 'storyObject' as it is undefined.
   * But only with "addon-svelte-csf",
   * 
   * https://github.com/storybookjs/addon-svelte-csf
  */
  const form = superForm(formValidated);
      
</script>


<Story name="Submit-button simple">
  
  <h1>Test</h1>
</Story>