Use EGL backend instead of Pyglet for renderer.py and renderer_xyz.py

change code to  template_labels[:162]
also change code to use self.extractor.find_correspondences not self.extractor.find_correspondences_fast..

also downloa the test folder from ycbv then put into folder test then change path  "dataset_path": "test/" in zs6d_configs/bop_eval_configs/cfg_ycbv_inference_bop.json

Then u can run test_zs6d.ipynb einwandfrei