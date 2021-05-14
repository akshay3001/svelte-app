<script>
  let usersPromise = getUsers();
  async function getUsers() {
    const usersResponse = await fetch('https://jsonplaceholder.typicode.com/users');
    const jsonResponse = await usersResponse.json();
    return jsonResponse;
  }
</script>

{#await usersPromise}
  <div class="border border-gray-100 shadow rounded-md p-4 w-full mx-auto">
  <div class="animate-pulse flex space-x-4">
    <div class="rounded-full bg-gray-100 h-12 w-12"></div>
    <div class="flex-1 space-y-4 py-1">
      <div class="h-4 bg-gray-100 rounded w-3/4"></div>
      <div class="space-y-2">
        <div class="h-4 bg-gray-100 rounded"></div>
        <div class="h-4 bg-gray-100 rounded w-5/6"></div>
      </div>
    </div>
  </div>
</div>

{:then users}
<div class="flex flex-col pt-10">
    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
        <div class="shadow-2xl overflow-hidden border-b border-gray-200 sm:rounded-lg">
          <table class="min-w-full divide-y divide-gray-200">
            <thead class="bg-gray-50">
              <tr>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Name
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Company
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Phone
                </th>
                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Username
                </th>
                <th scope="col" class="relative px-6 py-3 text-right text-xs font-medium text-gray-500 uppercase tracking-wider">
                  Website
                </th>
              </tr>
            </thead>
            {#each users as user}
              <tbody class="bg-white divide-y divide-gray-200">
                <tr class="hover:bg-gray-100">
                  <td class="px-6 py-4 whitespace-nowrap">
                    <div class="flex items-center">
                      <div class="flex-shrink-0 h-10 w-10">
                        <img class="h-10 w-10 rounded-full" src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=4&w=256&h=256&q=60" alt="">
                      </div>
                      <div class="ml-4">
                        <div class="text-sm font-medium text-gray-900">
                          {user.name}
                        </div>
                        <div class="text-sm text-gray-500">
                          {user.email}
                        </div>
                      </div>
                    </div>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <div class="text-sm text-gray-900">{user.company.name}</div>
                    <div class="text-sm text-gray-500">{user.company.bs}</div>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-green-100 text-green-800">
                      {user.phone}
                    </span>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                    {user.username}
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap text-right text-sm">
                    <!-- svelte-ignore a11y-missing-content -->
                    <a href={user.website} target="_blank" rel=”noopener>{user.website}</a>
                  </td>
                </tr>
              </tbody>
            {/each}
          </table>
        </div>
      </div>
    </div>
  </div>

{:catch error}
  Error
{/await}

<style>
  /* your styles go here */
</style>