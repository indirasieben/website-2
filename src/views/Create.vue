<template>
  <div id="Create" class="container">
    <el-row type="flex">
      <el-col
        ><div class="choose">{{ $t("create.chooseType") }}</div></el-col
      >
    </el-row>
    <el-row>
      <el-col :lg="8" :md="8" v-for="(item, index) in nftList" :key="index">
        <el-card
          class="item"
          :body-style="{ padding: '0px' }"
          shadow="hover"
          @click.native="getCreate(item.type)"
        >
          <el-image :src="item.img" class="image" lazy></el-image>
          <div style="padding: 14px">
            <div class="nft-name">{{ item.name }}</div>
            <div class="nft-tips">{{ item.tips }}</div>
          </div>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>
<script>
import { getToken, connect } from "@/utils/auth";
export default {
  name: "Create",
  data() {
    return {};
  },
  computed: {
    nftList() {
      return [
        {
          img: require("@/assets/images/create_0.png"),
          name: this.$t("create.singleNft"),
          tips: this.$t("create.supportSingleNFT"),
          type: "721",
        },
        {
          img: require("@/assets/images/create_1.png"),
          name: this.$t("create.multipleNfts"),
          tips: this.$t("create.supportMultipleNfts"),
          type: "m721",
        },
        {
          img: require("@/assets/images/create_2.png"),
          name: this.$t("create.SingleNftUp"),
          tips: this.$t("create.supportMultipleNumberNft"),
          type: "1155",
        },
      ];
    },
  },
  methods: {
    getCreate(type) {
      console.log(type);
      if (getToken()) {
        this.$router.push(`/upload?type=${type}`);
      } else {
        connect(() => {
          this.$router.push(`/upload?type=${type}`);
        });
      }
    },
  },
};
</script>
<style lang="less" scoped>
#Create {
  .choose {
    color: #000;
    font-size: 40px;
    font-weight: bold;
    margin: 80px 0;
    text-align: center;
  }
  .item {
    max-width: 308px;
    margin: 20px auto;
    cursor: pointer;
    img {
      width: 100%;
    }
    .nft-name {
      color: #000;
      font-size: 16px;
      font-weight: bold;
      margin-bottom: 10px;
    }
    .nft-tips {
      color: #999;
      font-size: 12px;
    }
  }
}
</style>
