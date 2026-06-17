<template>
  <header
    class="fixed left-0 top-0 z-50 w-full py-10 transition-all duration-500 max-lg:py-4"
  >
    <div class="container flex h-14 items-center max-lg:px-5">
      <div class="z-2 flex-1 lg:hidden">
        <a class="block w-fit cursor-pointer active">
          <img
            src="./assets/images/xora.svg"
            alt="xora logo"
            width="115"
            height="55"
          />
        </a>
      </div>
      <div
        class="w-full max-lg:fixed max-lg:left-0 max-lg:top-0 max-lg:w-full max-lg:bg-s2 max-lg:opacity-0 max-lg:pointer-events-none"
      >
        <div
          class="sidebar-before max-lg:relative max-lg:flex max-lg:min-h-screen max-lg:flex-col max-lg:overflow-hidden max-lg:p-6 max-md:px-4"
        >
          <nav class="max-lg:relative max-lg:z-2 max-lg:my-auto">
            <ul class="flex max-lg:block max-lg:px-12">
              <li class="nav-li">
                <a
                  class="base-bold max-lg:h5 cursor-pointer uppercase text-p4 transition-colors duration-500 hover:text-p1 max-lg:my-4"
                  >features</a
                >
                <div class="dot"></div>
                <a
                  class="base-bold max-lg:h5 cursor-pointer uppercase text-p4 transition-colors duration-500 hover:text-p1 max-lg:my-4"
                  >features</a
                >
              </li>
            </ul>
          </nav>
        </div>
      </div>
    </div>
  </header>
</template>
