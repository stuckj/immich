<script lang="ts">
  import { UserAvatarColor, type UserResponseDto } from '@immich/sdk';
  import { createEventDispatcher } from 'svelte';
  import FullScreenModal from '../full-screen-modal.svelte';
  import UserAvatar from '../user-avatar.svelte';

  export let user: UserResponseDto;

  const dispatch = createEventDispatcher<{
    close: void;
    choose: UserAvatarColor;
  }>();
  const colors: UserAvatarColor[] = Object.values(UserAvatarColor);
</script>

<FullScreenModal id="avatar-selector-modal" title="Select avatar color" width="auto" onClose={() => dispatch('close')}>
  <div class="flex items-center justify-center mt-4">
    <div class="grid grid-cols-2 md:grid-cols-5 gap-4">
      {#each colors as color}
        <button on:click={() => dispatch('choose', color)}>
          <UserAvatar label={color} {user} {color} size="xl" showProfileImage={false} />
        </button>
      {/each}
    </div>
  </div>
</FullScreenModal>
