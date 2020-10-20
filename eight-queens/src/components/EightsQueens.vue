<template>
  <div class="box">
    <div class="list" v-for="(item,index) in data" :key="index">
      <div
        class="item"
        v-for="(_item,_index) in item"
        :key="_index"
        @click.stop="select(index,_index)"
      >
        <div v-if="_item.active">Q</div>
      </div>
    </div>
  </div>
</template>
<style lang="less" scoped>
* {
  margin: 0;
  padding: 0;
}
.list {
  display: flex;
  .item {
    width: 50px;
    height: 50px;
    border-right: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
    text-align: center;
    line-height: 50px;
    &:first-child {
      border-left: 1px solid #ccc;
    }
  }
  &:first-child {
    .item {
      border-top: 1px solid #ccc;
    }
  }
  &:nth-child(2n) {
    .item {
      &:nth-child(2n) {
        background: #eee;
      }
      &:nth-child(2n-1) {
        background: #fff;
      }
    }
  }
  &:nth-child(2n-1) {
    .item {
      &:nth-child(2n) {
        background: #fff;
      }
      &:nth-child(2n-1) {
        background: #eee;
      }
    }
  }
}
</style>
<script>
const girds = new Array(8).fill( 1 ).map(( v, i ) => {
  return new Array( 8 ).fill( 1 ).map(( _v, _i ) => {
    return {
      key: `key-${ i * 8 + _i }`,
      active: false
    };
  });
});

export default {
  name: "EightQueens",
  data() {
    return {
      data: girds
    };
  },
  methods: {
    select( rindex, cindex ) {
      if ( this.validate( rindex, cindex ) ) {
        this.data[ rindex ][ cindex ].active = !this.data[ rindex ][ cindex ].active;
      } else {
        alert("当前位置不能放置皇后");
      }
    },
    validate( rindex, cindex ) {
      // 横
      for ( let i = 0; i < this.data[ rindex ].length; i++ ) {
        if ( this.data[ rindex ][ i ].active ) {
          return false;
        }
      }

      // 竖
      for ( let i = 0; i < this.data.length; i++ ) {
        if ( this.data[ i ][ cindex ].active ) {
          return false;
        }
      }

      // 撇
      for ( let i = 0; i < this.data[ 0 ].length; i++ ) {
        let y = rindex + cindex - i;
        if (y >= 0 && y < this.data.length && this.data[ y ][ i ].active ) {
          return false;
        }
      }

      // 捺
      for (let i = 0; i < this.data[ 0 ].length; i++ ) {
        let y = rindex - cindex + i;
        if ( y >= 0 && y < this.data.length && this.data[ y ][ i ].active ) {
          return false;
        }
      }

      return true;
    }
  }
};
</script>
