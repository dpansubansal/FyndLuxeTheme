<template>
  <div class="plp-wrapper section-margin-db"
    :style="global_config ? 'color:' + global_config.props.text_body_color : ''">
    <fdk-loader class="loader-ws" v-if="context.loading && (!context.items || context.items.length === 0)"></fdk-loader>
    <div v-else-if="
      !context.loading && (!context.items || context.items.length === 0)
    ">
      <fdk-empty-state :title="'No items found'"></fdk-empty-state>
    </div>
    <div v-else-if="context.page_error && context.page_error.statusCode === 500">
      <fdk-empty-state :title="'Something went wrong'"></fdk-empty-state>
    </div>
    <template style="scroll-behavior: smooth;" v-else-if="context && context.items">
      <h1 class="collection-title">{{ context.product_meta.name }}</h1>
      <div class="collection-desc">
        <!-- {{ is480width }} -->
        {{ context.product_meta.description }}
        <!-- {{ isMobile }} -->
      </div>
      <div class="mobile-header mobile">
        <div class="m-header">
          <div class="m-action-container" ref="mobileActionContainer">
            <div class="m-action-child-container" v-if="!is480width" v-on:click="viewModal($event, 'filter')">

              <div class="regular-xxxs">
                FILTER
                <span class="text-seperator"></span>
              </div>
              <div>
                <!-- FILTER ICON -->
                <svg width="13" height="12" viewBox="0 0 13 12" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path
                    d="M5.36667 12V8.25H6.36667V9.63333H12.25V10.6333H6.36667V12H5.36667ZM0.25 10.6333V9.63333H4.36667V10.6333H0.25ZM3.36667 7.86667V6.5H0.25V5.5H3.36667V4.1H4.36667V7.86667H3.36667ZM5.36667 6.5V5.5H12.25V6.5H5.36667ZM8.13333 3.75V0H9.13333V1.36667H12.25V2.36667H9.13333V3.75H8.13333ZM0.25 2.36667V1.36667H7.13333V2.36667H0.25Z"
                    fill="#26201A" />
                </svg>

              </div>
            </div>
            <div class="m-action-child-container" v-else v-on:click="viewModal($event, 'filter480')">

              <div class="regular-xxxs">
                FILTER
                <span class="text-seperator"></span>
              </div>
              <div>
                <!-- FILTER ICON -->
                <svg width="13" height="12" viewBox="0 0 13 12" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path
                    d="M5.36667 12V8.25H6.36667V9.63333H12.25V10.6333H6.36667V12H5.36667ZM0.25 10.6333V9.63333H4.36667V10.6333H0.25ZM3.36667 7.86667V6.5H0.25V5.5H3.36667V4.1H4.36667V7.86667H3.36667ZM5.36667 6.5V5.5H12.25V6.5H5.36667ZM8.13333 3.75V0H9.13333V1.36667H12.25V2.36667H9.13333V3.75H8.13333ZM0.25 2.36667V1.36667H7.13333V2.36667H0.25Z"
                    fill="#26201A" />
                </svg>

              </div>
            </div>
            <div class="m-action-child-container" v-on:click="viewModal($event, 'sort')">

              <div class="regular-xxxs">
                SORT
                <span class="text-seperator"></span>
              </div>
              <div>
                <svg width="10" height="12" viewBox="0 0 10 12" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path
                    d="M1.83398 11.3337H3.00065V3.33366H4.75065L2.41732 0.666992L0.0839844 3.33366H1.83398V11.3337ZM9.41732 8.66699H7.66732V0.666992H6.50065V8.66699H4.75065L7.08398 11.3337L9.41732 8.66699Z"
                    fill="#26201A" />
                </svg>

                <!-- SORT ICON -->
              </div>
            </div>

            <!-- <fdk-share class="m-action-child-container mobile">
              <template slot-scope="share">
                CMT SHARE ICON
                <div @click="getShareLink(share)" class="share-mobile-button">
                  <svg-wrapper :svg_src="'share'" class="share-mobile-img"></svg-wrapper>
                  <div class="regular-xxxs cl-DoveGray">
                    <span class="text-seperator"></span>
                    SHARE
                  </div>
                </div>
              </template>
            </fdk-share> -->
          </div>
        </div>
      </div>
      <div class="desktop-header desktop">
        <div class="header">
          <div class="m-action-container">
            <!-- <fdk-share class="m-action-child-container desktop">
              <template slot-scope="share">
                SHARE ICON comment
                <div @click="getShareLink(share)" class="share-mobile-button">
                  <svg-wrapper :svg_src="'share'" class="share-mobile-img"></svg-wrapper>
                  <transition name="fade desktop">
                    <share :title="`Spread the shopping delight! Scan QR & share this products with
                  your loved ones`" :shareLoading="shareLoading" :qr_code="qr_code" @close-share="showShare = false"
                      v-if="showShare && !isMobile" v-click-outside="hideShare" :share_link="share_link" />
                  </transition>
                  <div class="regular-sm cl-DoveGray">
                    <span class="text-seperator"></span>
                    DShare
                  </div>
                </div>
              </template>
            </fdk-share> -->
            <!-- <span class="text-seperator cl-DoveGray line">|</span> -->
            <!-- <div class="m-action-child-container" v-on:click="viewModal($event, 'filter')">
              <div>
                FILTER ICON Comment
                <svg-wrapper :svg_src="'filter'"></svg-wrapper>
              </div>
              <div class="regular-xxxs cl-DoveGray">
                <span class="text-seperator"></span>
                DFILTER
              </div>
            </div> -->
            <!-- v-click-outside="closeMyOption" -->
            <div class="left" v-click-outside="closeMyOption">
              <div class="filter-list" v-for="(filter, idx) in getFilters" :key="idx + '-desktop' + filter.key.display">
                <div class="filters">
                  <!-- <div class="filter-title regular-sm" v-on:click="filter.isOpen = !filter.isOpen" v-if="filter.values.length > 0"> -->
                  <div class="filter-title regular-sm" v-on:click="clickedFilter(idx)" v-if="filter.values.length > 0">
                    <span class="regular-xs cl-Mako fil_tit">{{ filter.key.display }}</span>
                    <span v-bind:class="{ 'filter-arrow-up': !filter.isOpen, }">
                      <!-- Arrow icon -->
                      <svg-wrapper :svg_src="'arrow-dropdown-black'"></svg-wrapper>
                    </span>
                  </div>
                  <div class="filter-disp filter-disp-adv" v-bind:class="{ open: filter.isOpen }"
                    v-if="filter.key.kind == 'multivalued'">
                    <!-- <div class="filter-search" v-if="filter.values.length > SHOW_SEARCH_THRESHOLD">
                    <input v-model="filter.searchText" :placeholder="placeholder" class="light-xxs"
                      @input="filterResults(filter, idx)" />
                    <span class="search-icon" @click="filterResults(filter, idx)">
                      <svg-wrapper :svg_src="'search-black'"></svg-wrapper>
                    </span>
                  </div> -->
                    <div class="example example-adv">
                      <ul class="filter-items-container filter-items-container-adv " id="scroll-bar">
                        <li v-for="(filterItem, index) in filter.filteredValues" :key="'filter-desktop' + index">
                          <fdk-link :link="filterItem.url">
                            <div class="filter-item filter-item-adv">
                              <div class="filter-item-i" v-if="!filterItem.is_selected">
                                <!-- CheckBox Unchecked -->
                                <!-- <svg-wrapper :svg_src="'regular'" class="icon"></svg-wrapper> -->
                                <div class="my__checkbox">
                                  <svg class="icon icon__check" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path
                                      d="M8.99988 16.8769L19.5899 6.29694L20.2929 7L9.00005 18.2929L4.11841 13.4112L4.8288 12.7059L8.99988 16.8769Z">
                                    </path>
                                  </svg>
                                </div>
                              </div>
                              <div v-if="filterItem.is_selected" class="filter-item-i">
                                <!-- CheckBox Checked -->
                                <div class="my__checkbox icon__filled">
                                  <svg class="icon icon__check" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path
                                      d="M8.99988 16.8769L19.5899 6.29694L20.2929 7L9.00005 18.2929L4.11841 13.4112L4.8288 12.7059L8.99988 16.8769Z">
                                    </path>
                                  </svg>
                                </div>
                                <!-- <svg-wrapper class="icon" :svg_src="'check-box-selected'"></svg-wrapper> -->
                              </div>

                              <div class="filter-item-value regular-xxs"
                                :class="{ active: filterItem.is_selected == true, }">
                                {{ filterItem.display }}
                              </div>
                              <!-- <div class="filter-item-count light-xxxs cl-DoveGray">
                              ({{ filterItem.count }})
                            </div> -->
                            </div>
                          </fdk-link>
                          <!-- <fdk-link :link="filterItem.url" v-else-if="viewMore[idx]">
                            <div class="filter-item">
                              <div v-if="!filterItem.is_selected">
                                CheckBox Unchecked
                                <svg-wrapper :svg_src="'regular'" class="icon"></svg-wrapper>
                              </div>
                              <div v-if="filterItem.is_selected">
                                CheckBox Checked
                                <svg-wrapper class="icon" :svg_src="'check-box-selected'"></svg-wrapper>
                              </div>

                              <div class="filter-item-value regular-xxs"
                                :class="{ active: filterItem.is_selected == true, }">
                                {{ filterItem.display }}
                              </div>
                              <div class="filter-item-count light-xxxs cl-DoveGray">
                                ({{ filterItem.count }})
                              </div>
                            </div>
                          </fdk-link> -->
                        </li>
                      </ul>
                      <!-- <div v-if="filter.filteredValues.length > 8" class="view-more" @click="changeViewMore(idx)">
                        {{ !viewMore[idx] ? `+ ${filter.filteredValues.length - 8} more` : `- view less` }}
                      </div> -->
                    </div>
                  </div>
                  <div class="filter-disp" v-bind:class="{ open: !filter.isOpen }"
                    v-else-if="filter.key.kind == 'range' && filter.values.length > 0">
                    <fdk-slider>
                      <template slot-scope="sliderData">
                        <fy-slider-filter :filteritem="filter" :reset="resetSlider" :show-text-box="false"
                          @slider-query="sliderData.replaceQuery($event, filter)"></fy-slider-filter>
                      </template>
                    </fdk-slider>
                  </div>
                  <div class="filter-disp" v-bind:class="{ open: !filter.isOpen }"
                    v-else-if="filter.key.kind == 'singlevalued' && filter.values.length > 0">
                    <fdk-link :link="filter.values[0].url">
                      <div class="filter-item">
                        <div v-if="!filter.values[0].is_selected">
                          <!-- CheckBox Unchecked -->
                          <svg-wrapper :svg_src="'regular'" class="icon"></svg-wrapper>
                        </div>
                        <div v-if="filter.values[0].is_selected">
                          <!-- CheckBox Checked -->
                          <svg-wrapper class="icon" :svg_src="'check-box-selected'"></svg-wrapper>
                        </div>

                        <div class="filter-item-value regular-xxs"
                          :class="{ active: filter.values[0].is_selected == true, }">
                          {{ filter.values[0].display }}
                        </div>
                        <div class="filter-item-count light-xxxs cl-DoveGray">
                          ({{ filter.values[0].count }})
                        </div>
                      </div>
                    </fdk-link>
                  </div>
                </div>
              </div>
            </div>
            <!-- <span class="text-seperator cl-DoveGray line">|</span> -->
            <!-- <div class="m-action-child-container DSort"> -->
            <div class="top_right_con">
              <sort-dd :filteredsorts="context.sort_on" :updateSelection="updateSelection" class="DSort" />
            </div>
          </div>
        </div>
      </div>
      <div class="content-container">
        <template>

          <div class="right">
            <div>
              <fdk-filter-modal>
                <template slot-scope="filterModalData">
                  <transition name="modal-filter" v-if="showFilterModal" @close="showFilterModal = !showFilterModal">
                    <div class="modal">
                      <div class="modal-container">
                        <div class="modal-header">
                          <span class="bold-xl">FILTER</span>
                          <div v-on:click="closeModal($event, 'filter'); filterModalData.closeModal();">
                            <svg-wrapper :svg_src="'cross-black'"></svg-wrapper>
                          </div>
                        </div>
                        <div class="modal-content">
                          <div class="pane leftPane">
                            <ul>
                              <li class="title" v-for="(filteritem, idx) in filterModalData.filters"
                                :key="idx + '-mobile'"
                                v-on:click="filterModalData.updateSelectedItem(filteritem, idx); mobileSearchText = '';">
                                <svg-wrapper v-if="!filteritem.key.logo" :svg_src="'home'"></svg-wrapper>
                                <!-- <img class="filter-image" v-else :src="filteritem.key.logo" alt="logo" /> -->
                                <span class="modal-text">
                                  {{ filteritem.key.display }}
                                </span>
                              </li>
                            </ul>
                          </div>
                          <div class="pane rightPane">
                            <div class="filter-disp"
                              v-if="filterModalData.filters[filterModalData.selected_item].key.kind !== 'range'">
                              <!-- <div class="filter-search-mobile"
                                v-if="filterModalData.filters[filterModalData.selected_item].values.length > SHOW_SEARCH_THRESHOLD">
                                <input type="text" v-model="mobileSearchText"
                                  :placeholder="'Search ' + filterModalData.filters[filterModalData.selected_item].key.display"
                                  @input="filterModalData.getFilteredResults(mobileSearchText)" />
                              </div> -->
                              <ul>
                                <li class="filterValue"
                                  v-for="(filterValue, index) in filterModalData.getFilteredResults(mobileSearchText)"
                                  :key="filterValue.value + index"
                                  v-on:click="filterModalData.updateFilter(filterValue, filterModalData.selected_item)">
                                  <!-- <svg-wrapper :svg_src="'regular'" class="icon" v-if="!filterValue.is_selected"></svg-wrapper>
                                  <svg-wrapper :svg_src="'check-box-selected'" class="icon" v-if="filterValue.is_selected"></svg-wrapper> -->
                                  <div class="filter-item-i" v-if="!filterValue.is_selected">
                                    <!-- CheckBox Unchecked -->
                                    <!-- <svg-wrapper :svg_src="'regular'" class="icon"></svg-wrapper> -->
                                    <div class="my__checkbox">
                                      <svg class="icon icon__check" viewBox="0 0 24 24"
                                        xmlns="http://www.w3.org/2000/svg">
                                        <path
                                          d="M8.99988 16.8769L19.5899 6.29694L20.2929 7L9.00005 18.2929L4.11841 13.4112L4.8288 12.7059L8.99988 16.8769Z">
                                        </path>
                                      </svg>
                                    </div>
                                  </div>
                                  <div v-if="filterValue.is_selected" class="filter-item-i">
                                    <!-- CheckBox Checked -->
                                    <div class="my__checkbox icon__filled">
                                      <svg class="icon icon__check" viewBox="0 0 24 24"
                                        xmlns="http://www.w3.org/2000/svg">
                                        <path
                                          d="M8.99988 16.8769L19.5899 6.29694L20.2929 7L9.00005 18.2929L4.11841 13.4112L4.8288 12.7059L8.99988 16.8769Z">
                                        </path>
                                      </svg>
                                    </div>
                                    <!-- <svg-wrapper class="icon" :svg_src="'check-box-selected'"></svg-wrapper> -->
                                  </div>
                                  <span class="regular-s">
                                    {{ filterValue.display }}
                                  </span>
                                  <!-- <span class="count regular-xxs">
                                    {{ filterValue.count }}
                                  </span> -->
                                </li>
                              </ul>
                            </div>

                            <div class="filter-disp" v-else>
                              <div class="slider">
                                <fy-slider-filter :filteritem="filterModalData.filters[filterModalData.selected_item]"
                                  :reset="resetSlider" :show-text-box="false"
                                  @slider-query="filterModalData.updateSliderInfo($event, filterModalData.filters[filterModalData.selected_item])">
                                </fy-slider-filter>
                              </div>
                            </div>
                          </div>
                        </div>
                        <div class="modal-footer">
                          <div class="actionBtn"
                            @click="filterModalData.resetFilters(); resetSlider = !resetSlider; filterModalData.applyFilters(); showFilterModal = false;">
                            <span>CLEAR ALL</span>
                          </div>
                          <div class="actionBtn actionBtnOk"
                            @click="filterModalData.applyFilters(); closeModal($event, 'filter');">
                            <span>APPLY</span>
                          </div>
                        </div>
                      </div>
                    </div>
                  </transition>
                </template>
              </fdk-filter-modal>
            </div>
            <div>
              <fdk-filter-modal>
                <template slot-scope="filterModalData">
                  <transition name="modal-filter" v-if="showFilter480Modal"
                    @close="showFilter480Modal = !showFilter480Modal">
                    <div class="modal">
                      <div class="modal-container">
                        <div class="modal-header">
                          <span class="bold-xl">FILTER480</span>
                          <div v-on:click="closeModal($event, 'filter480'); filterModalData.closeModal();">
                            <svg-wrapper :svg_src="'cross-black'"></svg-wrapper>
                          </div>
                        </div>
                        <div class="modal480-content">
                          <div class="paneHead480">
                            <ul>
                              <!-- <li class="title480" v-for="(filteritem, idx) in filterModalData.filters" :key="idx + '-mobile'" v-on:click="filterModalData.updateSelectedItem(filteritem, idx); mobileSearchText = '';"> -->
                              <li class="title480" v-for="(filteritem, idx) in filterModalData.filters"
                                :key="idx + '-mobile'">
                                <!-- <svg-wrapper v-if="!filteritem.key.logo" :svg_src="'home'"></svg-wrapper> -->
                                <!-- <img class="filter-image" v-else :src="filteritem.key.logo" alt="logo" /> -->
                                <div class="modal-text modal-text-adv"
                                  v-on:click="clickedFilter480(filterModalData, idx)">
                                  <div class="bold-lg active">
                                    {{ filteritem.key.display }}
                                  </div>
                                  <!-- {{ printConsole(filterModalData.filters) }} -->
                                  <div v-bind:class="{ 'filter-arrow-up': !filteritem.isOpen, }">
                                    <!-- Arrow icon -->
                                    <svg-wrapper :svg_src="'arrow-dropdown-black'"></svg-wrapper>
                                  </div>
                                </div>

                                <div class="pane480 rightPane480">
                                  <div class="filter480-disp" v-bind:class="{ open: filteritem.isOpen }"
                                    v-if="filteritem.key.kind !== 'range'">
                                    <ul>
                                      <li class="filterValue filter480value"
                                        v-for="(filterValue, index) in filteritem.values"
                                        :key="filterValue.value + index"
                                        v-on:click="filterModalData.updateFilter(filterValue, idx); mobileSearchText = '';">
                                        <div class="filter-item-i" v-if="!filterValue.is_selected">
                                          <div class="my__checkbox">
                                            <svg class="icon icon__check" viewBox="0 0 24 24"
                                              xmlns="http://www.w3.org/2000/svg">
                                              <path
                                                d="M8.99988 16.8769L19.5899 6.29694L20.2929 7L9.00005 18.2929L4.11841 13.4112L4.8288 12.7059L8.99988 16.8769Z">
                                              </path>
                                            </svg>
                                          </div>
                                        </div>
                                        <div v-if="filterValue.is_selected" class="filter-item-i">

                                          <div class="my__checkbox icon__filled">
                                            <svg class="icon icon__check" viewBox="0 0 24 24"
                                              xmlns="http://www.w3.org/2000/svg">
                                              <path
                                                d="M8.99988 16.8769L19.5899 6.29694L20.2929 7L9.00005 18.2929L4.11841 13.4112L4.8288 12.7059L8.99988 16.8769Z">
                                              </path>
                                            </svg>
                                          </div>
                                        </div>
                                        <span class="regular-s"
                                          v-bind:class="{ 'bold-lg active': filterValue.is_selected, }">
                                          {{ filterValue.display }}
                                        </span>
                                      </li>
                                    </ul>
                                  </div>

                                  <div class="filter-disp" v-else>
                                    <div class="slider">
                                      <fy-slider-filter :filteritem="filteritem" :reset="resetSlider"
                                        :show-text-box="false"
                                        @slider-query="filterModalData.updateSliderInfo($event, filteritem)">
                                      </fy-slider-filter>
                                    </div>
                                  </div>
                                </div>


                              </li>
                            </ul>

                          </div>


                        </div>
                        <div class="modal-footer">
                          <div class="actionBtn"
                            @click="filterModalData.resetFilters(); resetSlider = !resetSlider; filterModalData.applyFilters(); showFilter480Modal = false;">
                            <span>DISCARD</span>
                          </div>
                          <div class="actionBtn actionBtnOk"
                            @click="filterModalData.applyFilters(); closeModal($event, 'filter480');">
                            <span>APPLY</span>
                          </div>
                        </div>
                      </div>
                    </div>
                  </transition>
                </template>
              </fdk-filter-modal>
            </div>

            <!-- <fdk-infinite-loading class="plp-container">
              <template slot-scope="infiniteLoaderData">
                <div class="product-container">
                  <div v-for="(product, index) in getProducts" :key="index + '-product.uid'">
                    <div @click="redirectToProduct(product.url)" class="product-wrapper">
                      {{ product }}
                      <fy-product-card :product="product" :context="context" :active-product-id="active_product_uid"
                        @slide-up="slideUpEventListener($event)" @slide-down="slideDownEventListener($event)"
                        :global_config="global_config" :listing_price_config="listingPriceConfig"></fy-product-card>
                    </div>
                  </div>
                  <fdk-loader id="loader" class="loader-center" v-if="infiniteLoaderData.hasNext"></fdk-loader>
                </div>
              </template>
            </fdk-infinite-loading> -->


            <div class="infineOn xyz">
              <div class="filter-pill-container" v-show="getSelectedFilters.length">
                <div class="selected-filter-pill-container">
                  <div class="selected-filter-pill" v-for="(selectedFilter, index) in getSelectedFilters" :key="index">
                    <span>{{ selectedFilter.display }}</span>
                    <fdk-link :link="selectedFilter.url">
                      <img src="../../assets/images/close-icon.png" class="cancel-pill" />
                    </fdk-link>
                  </div>
                </div>

                <fdk-link :link="$route.path">
                  <span class="clear-filter-btn" @click="showFilter = false">CLEAR ALL</span>
                </fdk-link>
              </div>
              <!-- {{ getSelectedFilters }} -->
              <fdk-infinite-loading class="plp-container">
                <!-- <template slot-scope="infiniteLoaderData"> -->
                <div class="product-container">
                  <div v-for="(product, index) in filterProducts8" :key="index + '-product.uid'">
                    <div @click="redirectToProduct(product.url)" class="product-wrapper">
                      <!-- {{ product }} -->

                      <fy-product-card :product="product" :context="context" :showWishlist="true"
                        :active-product-id="active_product_uid" @slide-up="slideUpEventListener($event)"
                        @slide-down="slideDownEventListener($event)" :global_config="global_config"
                        :listing_price_config="listingPriceConfig"></fy-product-card>
                    </div>
                  </div>
                  <!-- <fdk-loader id="loader" class="loader-center" v-if="infiniteLoaderData.hasNext"></fdk-loader> -->
                </div>
                <!-- </template> -->
              </fdk-infinite-loading>

              <banner-db :bnr_img1="getPageConfigById('image1')" :bnr_img2="getPageConfigById('image2')"
                :bnr_head="getPageConfigById('bHead')" :bnr_subhead="getPageConfigById('bSubHead')"
                :btn_txt="getPageConfigById('button_text')" :btn_link="getPageConfigById('button_link')" />

              <!-- <div class="banner3">
                <div class="banner3_item banner3_item_1"><img :src="getPageConfigById('image1')" /></div>
                <div class="banner3_item banner3_item_2">
                  <div class="banner_text">

                    <div class="bnr_head">{{ getPageConfigById('bHead') }}</div>
                    <div class="bnr_sub">{{ getPageConfigById('bSubHead') }}</div>
                    <div class="bnr_btn">
                      <fdk-link :link="getPageConfigById('button_link')">
                        <div v-if="getPageConfigById('button_text')">{{ getPageConfigById('button_text') }}</div>
                      </fdk-link>
                    </div>
                  </div>
                </div>
                <div class="banner3_item banner3_item_3"><img :src="getPageConfigById('image2')" /></div>
              </div> -->
              <fdk-infinite-loading class="plp-container">
                <!-- <template slot-scope="infiniteLoaderData"> -->
                <div class="product-container">
                  <div v-for="(product, index) in filterProducts8plus" :key="index + '-product.uid'">
                    <div @click="redirectToProduct(product.url)" class="product-wrapper">
                      <!-- {{ product }} -->
                      <fy-product-card :product="product" :showWishlist="true" :context="context"
                        :active-product-id="active_product_uid" @slide-up="slideUpEventListener($event)"
                        @slide-down="slideDownEventListener($event)" :global_config="global_config"
                        :listing_price_config="listingPriceConfig"></fy-product-card>
                    </div>
                  </div>
                  <!-- <fdk-loader id="loader" class="loader-center" v-if="infiniteLoaderData.hasNext"></fdk-loader> -->
                </div>
                <!-- </template> -->
              </fdk-infinite-loading>
            </div>

            <!-- pagiiiiiiiiiiiiiiiiiiinnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnnggggggggggggggggggggggg -->
            <!-- <div class="infOff paging">
            <fdk-infinite-loading class="plp-container" :handleinfinite=true>
              <template slot-scope="infiniteLoaderData">
                <div class="product-container">
                  {{ context.selectedFilters }}
                  <div v-for="(product, index) in getProducts" :key="index + '-product.uid'">
                    <div @click="redirectToProduct(product.url)" class="product-wrapper">

                      <h1>hey</h1>
                      <fy-product-card :product="product" :context="context" :active-product-id="active_product_uid"
                        @slide-up="slideUpEventListener($event)" @slide-down="slideDownEventListener($event)"
                        :global_config="global_config" :listing_price_config="listingPriceConfig"></fy-product-card>
                    </div>
                  </div>
                  <button v-if="infiniteLoaderData.hasNext" @click="infiniteLoaderData.loadmore">next</button>
                  <fdk-loader id="loader" class="loader-center" v-if="infiniteLoaderData.hasNext"></fdk-loader>
                </div>
              </template>
            </fdk-infinite-loading>
          </div> -->
          </div>
        </template>
      </div>
      <transition name="modal-sort" v-if="showSortByModal">
        <div class="modal">
          <div class="modal-container">
            <div class="modal-header">
              <span class="bold-xl">Sort</span>
              <div v-on:click="closeModal($event, 'sort')">
                <svg-wrapper :svg_src="'cross-black'"></svg-wrapper>
              </div>
            </div>
            <div class="modal-content">
              <!-- <ul style="width: 100%">
                <li v-for="(sortitem, index) in context.sort_on" :key="index + '-sort'"
                  v-bind:class="{ 'bold-lg active': getSortOnValue == sortitem.value, }"
                  v-on:click="closeModal($event, 'sort')">
                  <fdk-link :link="sortitem.url" class="filterValue sort-item">
                    {{ sortitem.display }}
                    <sp an class="sort-arrow">
                      <svg-wrapper :svg_src="'arrow-dropdown-black'"></svg-wrapper>
                    </sp>
                  </fdk-link>
                </li>
              </ul> -->
              <ul style="width: 100%">
                <li v-for="(sortitem, index) in context.sort_on" :key="index + '-sort'"
                  v-bind:class="{ 'bold-lg active': getSortOnValue == sortitem.value, }"
                  v-on:click="closeModal($event, 'sort')">
                  <fdk-link :link="sortitem.url" class="filterValue sort-item">
                    <sp an class="sort-arrow">
                      <svg-wrapper :svg_src="'radio-selected'" v-if="getSortOnValue == sortitem.value"></svg-wrapper>
                      <svg-wrapper v-else :svg_src="'regular'"></svg-wrapper>
                    </sp>
                    {{ sortitem.display }}
                  </fdk-link>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </transition>
      <!-- FILTER MODAL -->
      <div class="mobile share-wrap">
        <transition name="fade" :data-ss="String(showShare)" :data-ismobile="String(isMobile)">
          <share :title="`Spread the shopping delight! Scan QR & share this products with
          your loved ones`" :shareLoading="shareLoading" :qr_code="qr_code" @close-share="showShare = false"
            v-if="showShare && isMobile" :share_link="share_link" v-click-outside="hideShare" :key="'mobile-share'" />
        </transition>
      </div>
      <back-to-top-db class="b2top" />
      <!-- <a href="#" class="back2top">&#8593;</a> -->
    </template>
  </div>
</template>

<settings>
{
  "props": [
    {
      "type": "checkbox",
      "id": "pCount",
      "label": "Show product count",
      "default": true,
      "info": "Check to "
    },
    {
      "type": "checkbox",
      "id": "InfScroll",
      "label": "Enable infinity scroll",
      "default": true,
      "info": "Check to "
    },
    {
      "type": "checkbox",
      "id": "back2top",
      "label": "Back to top button",
      "default": true,
      "info": "Check to "
    },
    {
            "type": "image_picker",
            "id": "image1",
            "default": "",
            "label": "Image 1",
            "info": "Pls attach Image"
    },
    {
            "type": "image_picker",
            "id": "image2",
            "default": "",
            "label": "Image 2",
            "info": "Pls attach Image"
    },
    {
            "type": "text",
            "id": "bHead",
            "default": "Explore Our Outfits",
            "label": "Banner Heading"
    },
    {
            "type": "text",
            "id": "bSubHead",
            "default": "Curated list of our best outfit combinations designed by Vastrakala experts",
            "label": "Banner Subheading"
    },
    {
            "type": "text",
            "id": "button_text",
            "default": "Read article",
            "label": "Button Text"
      },
      {
            "type": "url",
            "id": "button_link",
            "default": "",
            "label": "Button Link"
      }
  ]
}
</settings>

<script>
import fyproductcard from "./../../global/components/fy-product-card.vue";
import fyselect from "./../../global/components/fy-select.vue";
import fynotfound from "./../../global/components/fy-not-found.vue";
import sliderfilter from "./../../global/components/fy-slider-filter.vue";
import share from "./../../global/components/share.vue";
import { detectMobileWidth, detect480Width } from "./../../helper/utils";
import { isBrowser, isNode } from "browser-or-node";
import SvgWrapper from "./../../components/common/svg-wrapper.vue";
import sortDD from "./../../global/components/plp/sort-dd";
import bannerDB from "./../../global/components/plp/banner-db";
import backToTopDB from "./../../global/components/plp/back-to-top-db";



export default {
  name: "fdk-plp",
  components: {
    "fy-product-card": fyproductcard,
    "fy-select": fyselect,
    "fy-not-found": fynotfound,
    "fy-slider-filter": sliderfilter,
    "sort-dd": sortDD,
    "banner-db": bannerDB,
    share,
    "svg-wrapper": SvgWrapper,
    "back-to-top-db": backToTopDB,
  },
  props: {
    context: {
      type: Object
    },
    page_config: {
      type: Object
    }
  },

  watch: {
    context: function () {
      if (
        this.context.filters &&
        this.context.filters.length > this.viewMore.length
      ) {
        for (var i = 0; i < this.context.filters.length; i++) {
          if (!this.viewMore[i]) {
            this.$set(this.viewMore, i, false);
          }
        }
      }
    },
    active_product_uid: function () {
      this.context.item.map((item) => {
        if (item.uid === this.active_product_uid) {
          item.is_active = true;
        } else {
          item.is_active = false;
        }
      });
    },
  },
  data: function data() {
    return {
      shareLoading: false,
      showShare: false,
      share_link: "",
      qr_code: "",
      active_product_uid: 0,
      mobileSearchText: "",
      selectedSortOpt: "",
      storeName: "",
      SHOW_SEARCH_THRESHOLD: 8,
      placeholder: "Search ",
      showFilterModal: false,
      showSortByModal: false,
      filteredItems: [],
      selectedFilters: [],
      searchTextObj: {},
      resetSlider: false,
      viewMore: [],
      products: [
        {
          isImageLoading: true,
        },
      ],
      isMobile: false,
      showFilter: false,
      isMyMobile: false,
      showFilter480Modal: false,
    };
  },
  mounted() {
    this.isMobile = detectMobileWidth();
    this.is480width = detect480Width();
  },
  methods: {
    closeMyOption(event) {
      for (let i = 0; i < this.getFilters.length; i++) {
        this.getFilters[i].isOpen = true;
      }
    },
    printConsole(dataa) {
      console.log(dataa);
    },
    clickedFilter(idx) {
      for (let i = 0; i < this.getFilters.length; i++) {
        if (idx == i) {
          this.getFilters[i].isOpen = !this.getFilters[i].isOpen;
        }
        else {
          this.getFilters[i].isOpen = true;
        }
      }
    },
    clickedFilter480(filterModalData, idx) {
      console.log("runn+");
      filterModalData.filters[idx].isOpen = !filterModalData.filters[idx].isOpen;
      console.log("AfterFxnrunn+");
      console.log(filterModalData.filters);
    },
    toggleFilter() {
      this.showFilter = !this.showFilter;
    },
    hideShare() {
      this.showShare = false;
    },
    getShareLink(share) {
      this.shareLoading = true;
      this.showShare = true;
      share.getShareLink(window.location.href).then((res) => {
        share.generateQRCode(res).then((data) => {
          this.qr_code = `
                <div style="width: 250px;">
                  ${data.svg}
                </div>
                `;
          this.share_link = res;
          this.shareLoading = false;
        });
      });
    },
    slideUpEventListener(id) {
      this.active_product_uid = id;
    },
    slideDownEventListener() {
      this.active_product_uid = 0;
    },
    resetFilters(modalReset) {
      if (this.$refs && this.$refs.mobileActionContainer) {
        modalReset();
      }
      this.$router.push({ query: {} });
    },
    selectedOptions: function (context) {
      let { filters } = context;
      filters = filters || [];
      let filterOptionsArray = filters.reduce((a, f, index) => {
        let { values, key } = f;
        values = values || [];
        let selectedValues = values
          .map((v) => {
            if (v.is_selected) {
              v.filterIndex = index;
              return v;
            }
          })
          .filter((v) => v);
        return [...a, ...selectedValues];
      }, []);
      this.activeFilters = filterOptionsArray;
      return filterOptionsArray;
    },
    updateSelectedOptions(item, modalUpdate) {
      if (this.$refs && this.$refs.mobileActionContainer) {
        modalUpdate(item, item.filterIndex);
      }
      if (item.url) {
        this.$router.push(item.url);
      } else {
        this.getRangeURL(item);
      }
    },
    getRangeURL(item) {
      let key = this.context.filters[item.filterIndex].key.name;
      let q = { ...this.$route.query };
      if (Object.keys(q).includes(key)) {
        delete q[key];
      }
      this.$router.push({ ...this.$route, query: q });
    },

    getFilterDisplay: function getFilterDisplay(filters, filterObj) {
      let filter = filters[filterObj.filterIndex];
      console.log("hey wassup");
      console.log("the filter iss", filter);
      if (filter.key.kind === "range") {
        if (filterObj.currency_code) {
          return (
            "₹ " + filterObj.selected_min + " - ₹ " + filterObj.selected_max
          );
        } else {
          return filterObj.selected_min + "% - " + filterObj.selected_max + "%";
        }
      }
      return filterObj.display.toUpperCase();
    },
    changeViewMore(idx) {
      this.viewMore[idx] = !this.viewMore[idx];
      this.$forceUpdate();
    },
    kFormatter: function kFormatter(num) {
      return Math.abs(num) > 999
        ? Math.sign(num) * (Math.abs(num) / 1000).toFixed(2) + "k"
        : Math.sign(num) * Math.abs(num);
    },
    updateSelection: function updateSelection(val) {
      const sortItemIndex = this.context.sort_on.findIndex(
        (item) => item.value === val
      );
      this.$router.push(this.context.sort_on[sortItemIndex].url);
    },
    closeModal: function closeModal(event, type) {
      if (type === "sort") {
        this.showSortByModal = false;
      } else if (type === "filter") {
        this.showFilterModal = false;
      } else if (type === "filter480") {
        this.showFilter480Modal = false;
      }
    },
    viewModal: function viewModal(event, type) {
      if (type === "sort") {
        this.showSortByModal = true;
      } else if (type === "filter") {
        this.showFilterModal = true;
      } else if (type === "filter480") {
        this.showFilter480Modal = true;
      }
    },

    filterResults: function filterResults(filter, index) {
      this.getFilters[index].filteredValues = filter.values.filter((item) => {
        if (filter.searchText.length > 0) {
          this.searchTextObj[this.getFilters[index].key.name] =
            filter.searchText;
          return (
            item.display
              .toLowerCase()
              .indexOf(filter.searchText.toLowerCase()) !== -1
          );
        } else {
          return item;
        }
      });
      this.$forceUpdate();
    },
    loadImage: function loadImage(id) {
      const placeHolder = this.$refs[`placeholder-${id}`];
      placeHolder[0].style.display = "none";
    },
    redirectToProduct: function redirectToProduct(productUrl) {
      if (this.isLoadedInIframe()) {
        this.$router.push(productUrl);
        return;
      }
      if (!this.isMobile) {
        let routeData = this.$router.resolve(productUrl);
        window.open(routeData.href, "_blank");
      } else {
        this.$router.push(productUrl);
      }
    },
    isLoadedInIframe() {
      if (isBrowser && window.location !== window.parent.location) {
        return true;
      } else {
        return false;
      }
    },
    getPageConfigById(id) {
      return this.page_config?.props?.[id] || "";
    },
  },

  computed: {

    getFilters: function getFilters() {
      this.filteredItems = [];
      const data =
        this.context.filters &&
        this.context.filters.map((item) => {
          item.searchText =
            this.searchTextObj[item] && this.searchTextObj[item.key]
              ? this.searchTextObj[item.key.name]
              : "";
          item.filteredValues = item.values;
          this.filteredItems.push(item);

          return item;
        });
      return this.filteredItems;
    },
    getSortOnValue: function getSortOnValue() {
      let val = "";
      let item = [];
      if (this.context && this.context.sort_on) {
        item = this.context.sort_on.filter((item) => item.is_selected);
      }
      return item.length > 0 ? item[0].value : "popular";
    },
    // getSelectedFilters: function getSelectedFilters() {
    //   this.selectedFilters = this.getFilters.filter((item) => {
    //     return item.is_selected;
    //   });
    //   this.selectedFilters;
    // },
    // getSelectedFilters: function getSelectedFilters() {
    //   this.selectedFilters = this.getFilters.filter((item) => {
    //     return item.is_selected;
    //   });
    // },
    getSelectedFilters() {
      let selectedFilters = [];

      this.getFilters.forEach((item) => {
        selectedFilters = [...selectedFilters, ...item.filteredValues];
      });

      return selectedFilters.filter((item) => item.is_selected);
    },
    getProducts: function getProducts() {
      return this.context.items.map((item) => {
        item.is_active = false;
        return item;
      });
    },
    hrefTarget() {
      return this.isLoadedInIframe() ? "_self" : "_blank";
    },
    listingPriceConfig() {
      return this.context.app_features?.feature?.common?.listing_price?.value;
    },
    filterProducts8: function () {
      return this.getProducts.filter((item, index) => index < 8)
    },
    filterProducts8plus: function () {
      return this.getProducts.filter((item, index) => index >= 8)
    },
  },
};
</script>

<style lang="less" scoped>
.collection-title {
  text-align: left;
  font-size: 2.5rem;
  margin: 0.8rem auto 1rem;
}

.plp-container {
  @media @tablet {
    margin: 20px 0 0 0;
  }

  /deep/.list-items {
    background: none;
  }

  /deep/.loading {
    display: none;
  }
}

.share-wrap {
  /deep/ .share-popup {
    @media @tablet {
      top: 40px;
    }

    @media @mobile {
      top: 0;
    }
  }

  // @media mobile {
  //   display:none;
  // }
}


// .DSort{
//   /deep/.items{
//     margin: unset;
//     padding: unset;
//   }
// }

.share-button {
  margin-left: 10px;
  cursor: pointer;
  top: 7px;
  position: absolute;

  .share-img {
    position: relative;
    margin: 0;
  }
}

.share-mobile-button {
  cursor: pointer;
  display: flex;
  position: absolute;
  cursor: pointer;

  .share-mobile-img {
    position: relative;
    margin: 0;
  }
}

.content-container {
  display: flex;
  flex-direction: column;
  background: white;
  // margin-top: 15px;
  min-height: 80vh;

  @media @mobile {
    // margin: 10px 5px;
  }
}

.filterValue img,
.filter-item img {
  padding-right: 5px;
}

.desktop-header {
  padding: 0;
  display: flex;
  // line-height: 35px;
  align-items: center;
  background: none;

  margin-top: 20px;
  margin-bottom: 24px;
}

.cover .meta-desc {
  width: 130px;
}

.modal480-content {
  overflow: auto;
  height: 100%;
}

.title {
  width: 18%;
  text-transform: uppercase;
  line-height: 35px;
  margin: 0;
}

.title480 {
  border-bottom: 1px solid #ECE5DC;
  padding-bottom: 16px;
  padding-top: 16px;
  margin-left: 16px;
  margin-right: 16px;
}

.seperator {
  padding: 0 20px 0 24px;
  font-size: 21px;
  color: #41434c;
  opacity: 0.16;
}

.brand-name {
  text-transform: capitalize;
}

.sort {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin-left: auto;
  padding: 0 34px 0 0;
}

.sort-arrow {
  transform: rotate(-90deg);
}

.wide {
  width: 300px;
  min-height: 35px;
  margin-left: 0.3125rem;
  border: 0;
}

.store-name {
  font-weight: 900;
  margin-left: 0.5em;
}

.right {
  // margin: 1%;
  width: 100%;

  .collection-desc {
    margin: 1rem auto;
  }
}

.left {
  display: flex;
  // border-right: 1px solid #e4e5e6;
  // margin-bottom: 2em;
  // background-color: #ffffff;
}

.product-container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 1fr;
  grid-template-rows: 1fr;
  grid-gap: 2em;

  // @media screen and (max-width: 1024px) {
  //   grid-template-columns: repeat(auto-fill, minmax(30%, 1fr));
  // }

  /deep/ .imgClass {
    height: 100%;

    .fy__img {
      object-fit: contain;
    }
  }
}

// .product-wrapper {
//   border: 1px solid #e4e5e6;
//   border-radius: 3px;
//   box-sizing: border-box;
//   height: 100%;
// }

.mobile-header {
  display: none;

  //padding-bottom: 25px;
  .m-header {
    display: flex;
    flex-direction: column;
    background: white;
    justify-content: center;
    align-items: center;
    width: 100%;
    line-height: 2em;
    position: relative;
    z-index: 2;
    top: 0x;
    // border-top: 1px solid #f8f8f8;
  }

  .m-title {
    background: #f1f0ee;
    width: 100%;
    line-height: 20px;
  }

  .m-title>div {
    padding: 10px;
  }

  .text-seperator {
    padding: 0 5px;
  }

  .m-action-container {
    // margin-top:20px;
    width: 100%;
    display: flex;
    flex-direction: row;
    border-bottom: 1px solid #e6e6e6;   // disable for desktop
    text-align: center;
    color: #41434c;
    padding: 5px;
    user-select: none;
  }

  .m-action-child-container {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    border: groove #41434c 1px;

    /deep/ .share-popup {
      .close {
        top: 70px;
      }
    }
  }
}

.desktop-header {
  display: block;

  .header {
    display: flex;
    // flex-direction: column;
    background: white;
    // justify-content: center;
    // align-items: center;
    width: 100%;
    // line-height: 2em;
    // border-top: 1px solid #f8f8f8;
  }

  .m-title {
    background: #f1f0ee;
    width: 100%;
    line-height: 20px;
  }

  .m-title>div {
    padding: 10px;
  }

  .text-seperator {
    padding: 0 5px;
  }

  .m-action-container {
    // margin-top: 20px;
    width: 100%;
    display: flex;
    flex-direction: row;
    // border-bottom: 1px solid #e6e6e6;
    // text-align: center;
    color: #41434c;
    // padding: 5px 0;
    user-select: none;
    justify-content: space-between;
  }

  .m-action-child-container {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;

    /deep/ .share-popup {
      .close {
        top: 70px;
      }
    }
  }
}

.cl-DoveGray {
  color: #41434c;
}

.m-filter-container {
  width: 100%;
}

.line {
  height: 30px;
  line-height: 30px;
  color: #e6e6e6;
  top: 2px;
  font-size: 25px;
}

.filter-list {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  // width: 262px;
  /*background: white;*/
  // padding: 5px 10px;
  padding-right: 43px;
  min-height: auto;

}

.filter-item-value {
  text-transform: capitalize;
  font-size: 13px;
}

.filter-title {
  text-transform: uppercase;
  display: flex;
  flex-direction: row;
  // justify-content: space-between;
  align-items: center;
  // padding: 8px 0;
  cursor: pointer;
}

// .fil_tit {
// font-weight:bold !important;
// font-size:13px !important;
// }

.filter-arrow-up {
  transform: rotate(180deg);
}

.filter-item {
  display: flex;
  flex-direction: row;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  padding: 0 8px;
  align-items: center;
  min-height: 1.5rem;
  cursor: pointer;
  color: #41434c;
  // border-bottom: 1px solid #f5f5f5;
}

.filter-item-adv {
  padding: 0 20px;
}


.slider {
  padding: 20px;
}

.open {
  display: none;
}

.filter-search input {
  border: none;
  // background: #f5f5f5;
  outline: 0;
  padding: 7px 0 7px 5px;
  // border-radius: 5px 0 0 5px;
  width: 85%;
}

.search-icon {
  margin: auto;
}

.filter-search {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 0 0 10px 0;
  border: 1px solid #e4e5e6;
  // border-radius: 5px;
  cursor: pointer;
}

.filter-item-count {
  margin-left: auto;
}

.product-card {
  width: 100%;
  position: relative;
  border-radius: 5%;
}

.text-seperator {
  padding: 0 5px;
}

.modal {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 10;
  overflow: hidden;
  background-color: white;
  transition: all 0.25s ease;
  user-select: none;
}

.modal-container {
  height: 100vh;
}

.modal-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 32px;
}

.modal-content {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.modal-480content {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
}

.pane {
  height: 80vh;
  // overflow: auto;
}

.pane ul {
  padding-bottom: 30px;
  height: 75vh;
  overflow: auto;
}

.leftPane {
  flex: 0.6;
  border-right: 1px solid #e6e6e6;
  margin-left: 32px;
  background: rgba(241, 235, 229, 1);

}

.leftPane .title {
  display: flex;
  flex-direction: column;
  // align-items: center;
  align-items: flex-start;
  // padding: 12px 0;
  cursor: pointer;
  width: 100%;
  padding-left: 20px;
}

.leftPane .title:hover {
  // background-color: #e6e6e6;
  background: rgba(180, 171, 160, 1);

}

.inline-svg {
  margin-bottom: 0px;
  margin-right: 4px;
}

.rightPane {
  flex: 1.2;
}

.filterValue {
  // padding: 15px 10px;
  // border-bottom: 1px solid #e6e6e6;
  display: flex;
  align-items: center;
  padding: 1%;

  @media screen and (max-width: 480px) {
    padding: unset;
    padding-top: 12px;
    padding-left: 16px;
  }
}

.filterValue:hover {
  background-color: #e6e6e6;
}

// .sort-item {
// justify-content: space-between;
// }

.count {
  color: gray;
  margin-left: auto;
}

.filter-search-mobile {
  margin: 0 10px;
  padding: 5px;
  // border-radius: 10px;
  border: 1px solid gray;
  position: relative;
  height: 24px;
}

.filter-search-mobile input {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  border: none;
  text-indent: 10px;
  width: 85%;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

.modal-footer {
  position: fixed;
  bottom: 5%;
  left: 0;
  right: 0;
  background: white;
  text-align: center;
  border-top: 1px solid #e6e6e6;
  z-index: 1;
  display: flex;
  justify-content: space-evenly;
}

.actionBtn {
  width: 44%;
  display: inline-block;
  padding: 15px 10px;
  border: 1px solid rgba(38, 32, 26, 1);
  color: var(--primaryColor);
}

.actionBtnOk {
  color: white;
  background: rgba(38, 32, 26, 1);
}

// .actionBtn:nth-child(1) {
//   border-right: 1px solid #e6e6e6;
// }

.modal-text {
  text-transform: capitalize;
  text-align: center;
}

.modal-text-adv {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0px 16px;
}

.rating {
  unicode-bidi: bidi-override;
  color: #c5c5c5;
  font-size: 20px;
  height: 20px;
  width: 110px;
  position: relative;
  padding: 0;
  text-shadow: 0px 1px 0 #a2a2a2;
  white-space: nowrap;
}

.bottom-layer {
  padding: 0;
  display: block;
  z-index: 0;
}

.top-layer {
  color: #e7711b;
  padding: 0;
  position: absolute;
  z-index: 1;
  display: block;
  top: 0;
  left: 0;
  overflow: hidden;
  height: inherit;
}

.active {
  color: var(--primaryColor);
}


.filter-disp {
  // applied by dipanshu
  position: absolute;
  z-index: 5;
  background-color: white;
}

.filter-disp-adv {
  overflow: auto;
  //display: flex;
  left: 0;
  width: 101%;
}

.example-adv {
  display: flex;
}

.filter-items-container-adv {
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  max-height: 204px;
}

.rightPane>.filter-disp {
  width: 100%;
}

.my__checkbox {
  align-items: center;
  border: 1px solid #000;
  display: flex;
  height: 12px;
  justify-content: center;
  transition: all .1s cubic-bezier(0, 0, .58, 1);
  width: 12px;
}

.icon__filled {
  background-color: #000;
}

.icon__check {
  fill: white;
  transition: fill .1s cubic-bezier(0, 0, .58, 1);
}

.filter-item-i {
  padding-right: 6px;
}

/deep/ .loader-center {
  grid-column-start: -1;
  grid-column-end: 1;

  .container {
    background-color: transparent;
  }
}

@media screen and (max-width: 1024px) {}

@media screen and (max-width: 780px) {
  .product-image {
    width: 100%;
  }

  .header {
    display: none;
  }

  .mobile-header {
    display: block;
    position: sticky;
    // top: 66px;
    z-index: 3;
  }

  .desktop-header {
    display: none;
  }

  .left {
    display: none;
  }

  .right {
    width: 100%;
    // margin: 0 15px;
  }

  .product-container {
    grid-template-columns: repeat(auto-fill, minmax(40%, 1fr));
    grid-gap: 0.5em;
  }

  .cl-Profit {
    color: #41434c;
  }

  .header {
    display: none;
  }

  .inline-svg {
    margin-bottom: 0;
  }
}

@media screen and (min-width: 320px) {
  .actionBtn {
    width: 40%;
  }
}

// .shine {
//   border: 2px solid #dbd9d92a;
//   border-radius: 2%;
//   background: #f6f7f8;
//   background-image: linear-gradient(
//     to right,
//     #f6f7f8 0%,
//     #e8e9eb 20%,
//     #f6f7f8 40%,
//     #f6f7f8 100%
//   );
//   background-repeat: no-repeat;
//   background-size: 100% 100%;
//   display: inline-block;
//   position: relative;

//   -webkit-animation-duration: 1s;
//   -webkit-animation-fill-mode: forwards;
//   -webkit-animation-iteration-count: infinite;
//   -webkit-animation-name: placeholderShimmer;
//   -webkit-animation-timing-function: linear;
// }

// @-webkit-keyframes placeholderShimmer {
//   0% {
//     background-position: -468px 0;
//   }

//   100% {
//     background-position: 468px 0;
//   }
// }
.view-more {
  font-size: 14px;
  display: flex;
  justify-content: center;
  margin-top: 5%;
  color: var(--primaryColor);
  cursor: pointer;
}

.active-filters-container {
  font-size: 12px;
  display: flex;
  flex-wrap: wrap;
  padding: 0px 0 10px 0;
  margin: 0 0px 18px 0px;

  /*border-bottom: 1px solid #e4e5e6;*/
  @media @mobile {
    margin: 0;
    padding: 10px;
  }

  .selected-item {
    transition: all 0.1s ease-in;
    height: 1.5em;
    background: #e4e4e4;
    border-radius: 4px;
    border: 1px solid #bdbdbd;
    padding: 7px 9px;
    margin: 0 12px 12px 0;
    display: flex;
    align-items: center;
    color: #41434c;
    cursor: pointer;

    &:hover {
      background: #41434c;
      color: white;

      .close-icon {
        background-image: url("../../assets/images/close-icon.png");
      }
    }

    .close-icon {
      background-image: url("../../assets/images/close-icon.png");
      width: 9px;
      height: 9px;
      display: inline-block;
      background-size: cover;
    }
  }
}

.filter-image {
  width: 35px;
}

.product-count {
  font-size: 18px;
  font-weight: 700;
}

.dark-sm {
  font-size: 12px;
}


// .banner3 {
//   display: grid;
//   grid-template-columns: repeat(12, 1fr);
//   position: relative;
//   padding: 48px 0px;
// }

// .banner3_item_1 {
//   height: 328px;
//   grid-column-start: 1;
//   grid-column-end: 5;
// }

// .banner3_item_2 {
//   height: 328px;
//   grid-column-start: 5;
//   grid-column-end: 9;
//   grid-row: 1;
//   background-color: rgba(236, 229, 220, 1);
//   text-align: center;

// }

// .banner_text {
//   padding-top: 25%;
//   padding-left: 10%;
//   padding-right: 10%;
// }

// .bnr_head {
//   font-family: Marcellus;
//   font-size: 32px;
//   font-weight: 400;
//   line-height: 36px;
//   letter-spacing: -0.02em;
// }

// .bnr_sub {
//   padding-top: 4px;
//   font-family: Inter;
//   font-size: 12px;
//   font-weight: 400;
//   line-height: 16px;
//   letter-spacing: 0em;
// }

// .bnr_btn {
//   padding-top: 40px;
//   text-transform: uppercase;
//   text-decoration: underline;
//   color: rgba(119, 118, 118, 1);
//   font-family: Inter;
//   font-size: 14px;
//   font-weight: 500;
//   line-height: 20px;
//   letter-spacing: -0.02em;
// }

// .banner3_item_3 {
//   height: 328px;
//   grid-column-start: 9;
//   grid-column-end: 13;
//   grid-row: 1;
// }


.filter-pill-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 20px 0;
  // border-bottom: 2px solid #b5cec9;
}

.selected-filter-pill-container {
  display: flex;
  flex-wrap: wrap;
}

.selected-filter-pill {
  transition: all 0.1s ease-in;
  font-family: "FuturaPT-Book", Arial, sans-serif;
  // text-transform: lowercase;
  padding: 7px 9px;
  margin-right: 8px;
  display: flex;
  align-items: center;
  background-color: rgba(241, 235, 229, 1);
  color: #223628;
  cursor: pointer;
  gap: 5px;
}

.cancel-pill {
  height: 12px;
  display: block;
}

// .banner3_item>img {
//   width: 100%;
//   height: 100%;
//   object-fit: cover;
// }

.top_right_con {
  // align-self: center;
}

// .back2top {
//   --offset: 50px;
//   position: sticky;
//   bottom: 32px;
//   margin-right: 10px;
//   place-self: end;
//   margin-top: calc(100vh + var(--offset));

//   /* visual styling */
//   text-decoration: none;
//   padding: 12px;
//   color: #26201A;
//   background: #FFFFFF;
//   // border-radius: 100px;
//   border-radius: 50%;
//   white-space: nowrap;
//   font-family: Inter;
//   font-size: 12px;
//   font-weight: 400;
//   line-height: 16px;
//   box-shadow: 0px 2px 4px 0px rgb(0 0 0 / 8%);
//   left: 90%;

//   @media screen and (max-width: 768px) {}
// }

// @media screen and (max-width: 780px) {
//   .banner3 {
//     grid-template-columns: auto auto;
//   }

//   .banner3_item_1 {
//     grid-column-start: 1;
//     grid-column-end: 5;
//   }

//   .banner3_item_2 {
//     grid-column-start: 5;
//     grid-column-end: 9;
//     text-align: left;
//   }

//   .banner_text {
//     padding-top: 25%;
//     padding-left: 146px;
//     padding-right: 10%;
//   }

//   .banner3_item_3 {
//     position: absolute;
//     height: 254px;
//     width: 171px;
//     align-self: center;
//     // grid-column: 3;
//     grid-column: 4;
//     top: 10%;
//   }

// }

// @media screen and (max-width: 480px) {
//   .banner3_item_1 {
//     grid-column-start: 1;
//     // grid-column-end: 11;
//   }

//   .banner3_item_3 {
//     grid-column: unset;
//     right: 0;
//     // top: 8%;
//     grid-row: 1;
//     align-self: unset;
//     top: unset;
//     bottom: 34%;
//   }

//   .banner3_item_2 {
//     grid-column-start: 1;
//     grid-column-end: 13;
//     grid-row: 2;
//     width: 100%;
//     background-color: unset;
//     height: unset;
//   }

//   .banner3_item_1>img {
//     height: unset;
//   }

//   .banner3_item_1 {
//     height: unset;
//   }

//   .banner_text {
//     padding: 16px 0px;
//   }


// }
</style>
