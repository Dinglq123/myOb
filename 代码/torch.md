# Tensor基本操作
## 张量某一维度复制
`tensor.repeat(1,2)`:在1维度上复制一次
## 张量数据类型转换
```python
tensor = torch.Tensor(3, 5)

# torch.long() 将tensor投射为long类型
newtensor = tensor.long()

# torch.half()将tensor投射为半精度浮点类型
newtensor = tensor.half()

# torch.int()将该tensor投射为int类型
newtensor = tensor.int()

# torch.double()将该tensor投射为double类型
newtensor = tensor.double()

# torch.float()将该tensor投射为float类型
newtensor = tensor.float()

# torch.char()将该tensor投射为char类型
newtensor = tensor.char()

# torch.byte()将该tensor投射为byte类型
newtensor = tensor.byte()

# torch.short()将该tensor投射为short类型
newtensor = tensor.short()

# 转换成其它tensor的数据类型：
a.type_as(b)
```
# 图像处理
## 双线性插值
```python
theta = torch.tensor([
    [1,0,0],
    [0,1,0]
], dtype=torch.float)
theta=theta.repeat(img_0.shape[0],1,1).cuda()
grid = F.affine_grid(theta,img_0.shape)
txt_0 = F.grid_sample(txt, grid)  #txt:(batch,64,87,32) 
```
## 图像的读取、可视化、转化为向量
```python
import PIL.Image
from torchvision import transforms


image=PIL.Image.open(file_path)
trans=transform.
tensor_image=
```
# 训练相关
## 训练基本流程
```python
# 模型搭建：
from torch import nn

class Model(nn.Module):
    def __init__(self) -> None:
        super().__init__()
        self.model=nn.Sequential(
            nn.Conv2d(in_channels=3,out_channels=32,kernel_size=5,stride=1,padding=2),
            nn.MaxPool2d(kernel_size=2),
            nn.Conv2d(in_channels=32,out_channels=32,kernel_size=5,stride=1,padding=2),
            nn.MaxPool2d(kernel_size=2),
            nn.Conv2d(in_channels=32,out_channels=64,kernel_size=5,padding=2),
            nn.MaxPool2d(kernel_size=2),
            nn.Flatten(),
            nn.Linear(in_features=1024,out_features=64),
            nn.Linear(in_features=64,out_features=10)
        )
    def forward(self,x):
        y=self.model(x)
        return y


# 损失函数及优化器：
optim=torch.optim.SGD(model.parameters(),lr=0.1)
loss=nn.CrossEntropy()
optim.zero_grad()
optim.step()


# 更改当前路径
import os
print(os.getcwd())#显示当前路径
 
os.chdir(os.getcwd()+os.sep+'TIPCB-main')#更改路径，''里面为更改的路径
 
print("更改后的当前路径： ",os.getcwd())#显示当前路径


# 从cuda转换为cpu:
tensor=tensor.cpu()
# 从cpu转换为gpu
tensor=tensor.cuda()

# 复制一个tensor，但是这个tensor不会进行反向传播
tensor.detach():
```
## 构建数据集
```python
from torch.utils.data import Dataset

class MyData(Dataset):
    
    def __init__(self):

    def __getitem__(self,idx):
    
    def __len__(self):
    
```
## 训练注意事项
```python
model.train()  # 训练时
model.eval()   # 测试时
```
## 模型保存与加载
```python
# 现有模型加载：
vgg16=torchvision.models.vgg16(pretrained=False)

# 模型保存加载参数方式一:（保存结构和数据）
torch.save(vgg16,"filepath"）
model=torch.load("filepath")

# 模型保存加载参数方式二:（只保存数据)
torch.save(vgg16.state_dict(),"filepath")
vgg16=torchvision.models.vgg16(pretrained=False)
vgg16.load_state_dict(torch.load("filepath"))

```
### 断点保存，重新训练
```python
#	权重保存函数
def save_checkpoint(model, epoch, optimizer, dst):
    if not os.path.exists(dst):
        os.makedirs(dst)
    checkpoint = {"model_state_dict": model.state_dict(),
                "optimizer_state_dict": optimizer.state_dict(),
                "epoch": epoch}
    path_checkpoint = os.path.join(dst, str(epoch)) + '.pth.tar'
    torch.save(checkpoint, path_checkpoint)

#	权重加载函数
def load_checkpoint(model,checkpoint_dir,optimizer,device='cuda'):
    start_epoch=0

    files=os.listdir(checkpoint_dir)
    names=[]
    for filename in files:
        if re.search(r'[0-9]+.pth.tar',filename):
            # print('成功')
            num,*_=filename.split('.')
            names.append(int(num))

    names.sort(reverse=True)

    filename=str(names[0])+".pth.tar"

    checkpoint = torch.load(os.path.join(checkpoint_dir,filename), map_location=device)
    load_weights_dict = {k: v for k, v in checkpoint['model_state_dict'].items()
                            if model.state_dict()[k].numel() == v.numel()}
    model.load_state_dict(load_weights_dict, strict=False)

    start_epoch = checkpoint['epoch']
    optimizer.load_state_dict(checkpoint['optimizer_state_dict'])
#优化器参数为了优化内存，映射到了cpu 需要手动转化为cuda
    for state in optimizer.state.values():
        for k, v in state.items():
            if torch.is_tensor(v):
                state[k] = v.cuda()
                
    if is_main_process():
        print('Load checkpoint at epoch %d.' % (start_epoch))
    return start_epoch,model,optimizer

start_epoch, model,optimizer = load_checkpoint(model, checkpoint_dir,optimizer, device=device)

scheduler = torch.optim.lr_scheduler.StepLR(optimizer, int(args.epoches_decay), gamma=args.lr_decay_ratio,last_epoch=epoch)
```
## 数据保存与可视化
```python
from torch.utils.tensorboard import SummaryWriter
# 基础：只保留一个变量的
writer=SummaryWriter("filepath")

writer.add_scalar("title",value,time)

writer.close()

#分级表示
writer=SummaryWriter("root1/root2")

# 两个变量画到同一个表里面
# writer要在同一个根目录下面，取不同的名字。 
# add_scalar的时候变量名要相同

writer1=SummaryWriter("root1/train")
writer2=SummaryWriter("root1/test")

writer1.add_scalar('loss',loss.train(),epoch)
writer2.add_scalar('loss',loss.test(),epoch)

# 显示
tensorboard --logdir=filepath --port=
```
## log打印
```python
class Logger_log():
    def __init__(self,fpath):
        self.file=None
        if fpath is not None:
            mkdir_if_missing(os.path.dirname(fpath))
            self.file = open(fpath, 'a')
    def write(self,str):
        self.file.write(str)
        
    def close(self):
        self.file.close()
```
## 多卡训练（DDP）
[参考链接](https://zhuanlan.zhihu.com/p/402198819)
待
## 释放显存
# 项目相关
## ViLT:图像文本直接输入到一个Bert里面
## SCAN：计算细粒度局部特征之间的相似度来聚合整体 图像-文本 的相似度
```python
# 相似度矩阵式N*M 其中N：图象数目 M：文本数目
# 以（shared_size,shared_size）的窗口移动，计算矩阵内的相似度
def shard_xattn_t2i(images, captions, caplens, opt, shard_size=128):
    """
    Computer pairwise t2i image-caption distance with locality sharding
    """
    n_im_shard = (len(images)-1)/shard_size + 1
    n_cap_shard = (len(captions)-1)/shard_size + 1
    
    d = np.zeros((len(images), len(captions)))
    for i in range(n_im_shard):
        im_start, im_end = shard_size*i, min(shard_size*(i+1), len(images))
        for j in range(n_cap_shard):
            sys.stdout.write('\r>> shard_xattn_t2i batch (%d,%d)' % (i,j))
            cap_start, cap_end = shard_size*j, min(shard_size*(j+1), len(captions))
            im = Variable(torch.from_numpy(images[im_start:im_end]), volatile=True).cuda()
            s = Variable(torch.from_numpy(captions[cap_start:cap_end]), volatile=True).cuda()
            l = caplens[cap_start:cap_end]
            sim = xattn_score_t2i(im, s, l, opt)
            d[im_start:im_end, cap_start:cap_end] = sim.data.cpu().numpy()
    sys.stdout.write('\n')
    return d
 
 # 计算矩阵内的相似度
 def xattn_score_t2i(images, captions, cap_lens, opt):
    """
    Images: (n_image, n_regions, d) matrix of images
    Captions: (n_caption, max_n_word, d) matrix of captions
    CapLens: (n_caption) array of caption lengths
    """
    similarities = []
    n_image = images.size(0)
    n_caption = captions.size(0)
    for i in range(n_caption):
        # Get the i-th text description
        n_word = cap_lens[i]
        cap_i = captions[i, :n_word, :].unsqueeze(0).contiguous()
        # --> (n_image, n_word, d)
        cap_i_expand = cap_i.repeat(n_image, 1, 1)
        """
            word(query): (n_image, n_word, d)
            image(context): (n_image, n_regions, d)
            weiContext: (n_image, n_word, d)
            attn: (n_image, n_region, n_word)
        """
        weiContext, attn = func_attention(cap_i_expand, images, opt, smooth=opt.lambda_softmax)
        cap_i_expand = cap_i_expand.contiguous()
        weiContext = weiContext.contiguous()
        # (n_image, n_word)
        row_sim = cosine_similarity(cap_i_expand, weiContext, dim=2)
        if opt.agg_func == 'LogSumExp':
            row_sim.mul_(opt.lambda_lse).exp_()
            row_sim = row_sim.sum(dim=1, keepdim=True)
            row_sim = torch.log(row_sim)/opt.lambda_lse
        elif opt.agg_func == 'Max':
            row_sim = row_sim.max(dim=1, keepdim=True)[0]
        elif opt.agg_func == 'Sum':
            row_sim = row_sim.sum(dim=1, keepdim=True)
        elif opt.agg_func == 'Mean':
            row_sim = row_sim.mean(dim=1, keepdim=True)
        else:
            raise ValueError("unknown aggfunc: {}".format(opt.agg_func))
        similarities.append(row_sim)

    # (n_image, n_caption)
    similarities = torch.cat(similarities, 1)
    
    return similarities
 
```
## ALBEF：先用对比学习拉进，再进行融合
```python
        # select a negative text for each image
        text_embeds_neg = []
        text_atts_neg = []
        for b in range(bs):
            neg_idx = torch.multinomial(weights_i2t[b], 1).item()
            text_embeds_neg.append(text_embeds[neg_idx])
            text_atts_neg.append(text.attention_mask[neg_idx])
        text_embeds_neg = torch.stack(text_embeds_neg,dim=0)   
        text_atts_neg = torch.stack(text_atts_neg,dim=0)     
```