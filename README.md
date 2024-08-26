This file summarizes the steps replicate the work presented in the paper **MST-KD: Multiple Specialized Teachers Knowledge Distillation for Fair Face Recognition**. The mentioned hyperparameters can be altered in the file config/config.py and **should be changed there** (some hyperparameters should be changed at specific steps to exactly mimic the paper results).

1. Run baseline_data_split.py four times (changing the cfg.ethnicity parameter) to perform a balanced datasplit of the trainset in four groups. Each subset will be used to train one of the four baseline teachers
2. Run train.py to train each of the teacher models. This script should be ran four times to obtain the four teacher models, changing the cfg.ethnicity parameter. To train the baseline teachers, set cfg.is_teacher_baseline to True
3. Run extract_all for the four ethnicities by changing the cfg.ethnicity parameter
4. To obtain the adaptors:
    4.1. Run fc_EArc.py once to obtain SL-EAF-Fusion
    4.2. Run dual_layer_EAF-Fusion.py twice to obtain DuL-EAF-Fusion (setting cfg.has_dropout=False) and DLDPO-EAF-Fusion (setting cfg.has_dropout=True)
5. To obtain the students, run KD_alone.py (for a-KD) or KD_CEL.py (for EAF-KD) with each of the following configurations:
    5.1. Set cfg.is_dual_layer to False to obtain SL-EAF-Fusion students
    5.2. Set cfg.is_dual_layer to True and cfg.has_dropout to False to obtain DuL-EAF-Fusion students
    5.3. Set cfg.is_dual_layer to True and cfg.has_dropout to True to obtain DLDPO-EAF-Fusion students