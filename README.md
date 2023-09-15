# MultiDAG
Using DAG + hybrid curriculum learning with multimodal data

### Datasets and Utterance Feature
You can download the dataset and extracted utterance feature from https://drive.google.com/drive/folders/1zCfjx-HhqEY2tQlxvg1X_6T7sB6hVA2T?usp=sharing. Multimodal datasets are only available for IEMOCAP and MELD, marking with "_mm" in their names.

## Training
To train model with all three modals (not using hybrid curriculum): 
`!python run.py --dataset_name IEMOCAP --gnn_layers 4 --lr 0.0005 --batch_size 16 --epochs 30 --dropout 0.4 --emb_dim 2948`
  (2948 = 1024 + 1582 + 342)
In read function (dataset.py): 
`features.append(u['cls'][0]+u['cls'][1]+u['cls'][2])`
To run program with text + visual: 
`!python run.py --dataset_name IEMOCAP --gnn_layers 4 --lr 0.0005 --batch_size 16 --epochs 30 --dropout 0.4 --emb_dim 1366`
  (1366 = 1024 + 342)
In read function (dataset.py):
`features.append(u['cls'][0]+u['cls'][2])`
Evaluate (required saving model first):
`!python evaluate.py --dataset_name IEMOCAP --state_dict_file /link/to/saved/model --gnn_layers 4 --lr 0.0005 --batch_size 16 --dropout 0.4 --emb_dim 2948`

To train model with curriculum learning: adding --hybrid_curriculum and --bucket_number parameter.
Train model with all three modals and curriculum learning: 
`!python run.py --dataset_name IEMOCAP --gnn_layers 4 --lr 0.0005 --batch_size 16 --epochs 30 --dropout 0.4 --emb_dim 2948 --hybrid_curriculum --bucket_number 12`


