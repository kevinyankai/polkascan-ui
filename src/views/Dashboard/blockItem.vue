<template>
  <div class="block-item-wrapper space-between">
    <div class="block-left">
      <div class="block-num align-items-center">
        <div class="label">Block#</div>
        <div
          class="value"
          @click="$router.push(`/block/${blockData.block_num}`)"
        >{{+blockData.block_num|toThousandslsFilter}}</div>
      </div>
      <div class="block-includes align-items-center">
        <div class="label">Includes</div>
        <div class="value">
          <div
            class="extrinsics"
            :class="{empty: blockData.extrinsics_count==0}"
          >{{blockData.extrinsics_count}} Extrinsics</div>
          <div
            class="event"
            :class="{empty: blockData.event_count==0}"
          >{{blockData.event_count}} Event</div>
        </div>
      </div>
    </div>
    <div class="block-right align-items-center">{{blockData.block_timestamp|timeAgo(currentTime)}}</div>
  </div>
</template>

<script>
import { timeAgo, toThousandslsFilter } from "Utils/filters";
export default {
  props: {
    blockData: {
      type: Object,
      required: true
    },
    currentTime: {
      type: Number
    }
  },
  filters: {
    timeAgo,
    toThousandslsFilter
  }
};
</script>

<style lang="scss" scoped>
.block-item-wrapper {
  box-sizing: border-box;
  height: 80px;
  padding: 16px 0 20px;
  .block-left {
    .block-num {
      transform: translateY(-3px);
      .label {
        font-size: 13px;
        font-weight: 600;
        color: rgba(19, 18, 18, 1);
      }
      .value {
        cursor: pointer;
        transform: translateY(-1px);
        font-size: 18px;
        font-weight: 600;
        color: var(--main-color);
      }
    }
    .block-includes {
      // padding-top: 1px;
      .label {
        font-size: 12px;
        font-weight: 600;
        color: rgba(152, 149, 159, 1);
      }
      .value {
        display: flex;
        font-size: 12px;
        font-weight: 400;
        color: var(--main-color);
        .event {
          margin-left: 10px;
        }
        .extrinsics,
        .event {
          cursor: pointer;
        }
        .extrinsics.empty,
        .event.empty {
          cursor: auto;
          color: rgba(152, 149, 159, 1);
        }
      }
    }
    .block-num,
    .block-includes {
      .label {
        width: 59px;
      }
    }
  }
  .block-right {
    font-size: 14px;
    font-weight: 600;
    color: rgba(152, 149, 159, 1);
  }
}
</style>