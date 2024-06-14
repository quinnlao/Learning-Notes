algorithm [ˈælɡəˌrɪðəm]


[乱序绝对值之和最小](https://blog.csdn.net/qq_25753445/article/details/124917801?ops_request_misc=&request_id=&biz_id=102&utm_term=%E4%B9%B1%E5%BA%8F%E6%95%B4%E6%95%B0%E5%BA%8F%E5%88%97%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C%E7%BB%9D%E5%AF%B9%E5%80%BC%E6%9C%80%E5%B0%8Fjs&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-124917801.142)


[分积木](https://www.nowcoder.com/discuss/957454?source_id=profile_create_nctrack&channel=-1)

[we are a team](https://www.nowcoder.com/discuss/934770?type=all&order=recall&pos=&page=1&ncTraceId=&channel=-1&source_id=search_all_nctrack&gio_id=2FD1FCFDF95E5CF9DD2D1FD9E9F1B906-1655541783689)

```javascript
class UnionFind {
    constructor(size) {
        this.fa = [];
        this.size = size;
        this.init();
    }
    // 初始化 每个元素的父节点为自身
    init() {
        for(let i = 0; i < this.size; i++) {
            this.fa[i] = i;
        }
    }
    // 递归找到根节点，同时进行路径压缩
    find(x) {
        if(x === this.fa[x]) {
            return x;
        }
        this.fa[x] = this.find(this.fa[x]);
        return this.fa[x];
    }
    // 合并 x, y 直到各自的根节点， 其中一个的指向另一个
    merge(x, y) {
        let fx = this.find(x);
        let fy = this.find(y);
        if(fx !== fy) {
            this.fa[fx] = fy;
        }
    }
    // 获取集合数量
    getCount() {
        let count = 0;
        for(let i = 0; i < this.size; i++) {
            if(this.fa[i] === i) {
                count++;
            }
        }
        return count;
    }
}
```
