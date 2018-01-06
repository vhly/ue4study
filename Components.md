# UE4 中的组件

## Volumes 体积

### NavMeshBoundVolume 自动移动体积

在这个里面的Character可以通过简单的调用，即可实现移动位置，并且自动包含显示边框<br/>
即把角色限制在一个区域内。<br/>

### LightmassImportanceVolume 重点光照体积

使用LightmassImportanceVolume可以告诉光照构建器，哪些地方是需要进行光照构建的，<br/>
角色必须在这个体积之内，在体积之外的不会构建阴影。
