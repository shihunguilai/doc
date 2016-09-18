# yac在php项目中的使用
[toc]
##yac简介
yac是php大神鸟哥写的本地缓存php扩展，他可以替换apc或者本地的memcached

##安装yac
- [安装教程](https://github.com/laruence/yac#yac---yet-another-cache)

## 在项目中的应用
>我的github：[https://github.com/shihunguilai/cliff/blob/master/Cache/cacheYac.php](https://github.com/shihunguilai/cliff/blob/master/Cache/cacheYac.php)

```
<?php
namespace Cliff\Cache;


class CacheYac
{
    private $have_extension = false;
    private $cache_pre = '';
    private $m = null;

    private static $instance = null;

    private function __construct()
    {
        $this->init();
    }

    private function init()
    {
//        echo 111;exit;
//        var_dump(extension_loaded('yac'));exit;
        if(extension_loaded('yac')){
            $this->have_extension = true;
            $this->m = new \Yac($this->cache_pre);

//            var_dump($this->m);exit;

        }
    }

    public static function getInstance()
    {
//        echo 11;exit;
        if(!(self::$instance && self::$instance instanceof self)){
            self::$instance = new self();
        }
        return self::$instance;
    }

    /**
     * @param string $name
     * @param mixed $value
     * @param int $ttl
     * @return bool
     */
    public function set($name,$value,$ttl = 0)
    {
        if(!$this->have_extension){return false;}
        $value = serialize($value);
        if(is_int($ttl) && $ttl){
            return $this->m->set($name,$value,$ttl);
        }
        return $this->m->set($name,$value);
    }


    /**
     * @param array $kvs
     * @param int $ttl
     * @return mixed
     */
    public function mSet(array $kvs,$ttl = 0)
    {
        if(!$this->have_extension){return false;}
        array_walk($kvs,function(&$val){
            $val = serialize($val);
        });
        if(is_int($ttl) && $ttl){
            return  $this->m->set($kvs,$ttl);
        }
        return $this->m->set($kvs);
    }


    /**
     * @param string | array $name
     * @return mixed
     */
    public function get($name)
    {
        if(!$this->have_extension){return null;}
        $tp = $this->m->get($name);
        if(is_string($name)){
            return unserialize($tp);
        }elseif (is_array($name)) {
            array_walk($tp,function(&$val){
                $val = unserialize($val);
            });
            return $tp;
        }
    }

    /**
     * @param  string | array $name
     * @param int $delay
     * @return mixed
     */
    public function rm($name,$delay = 0)
    {
        if(!$this->have_extension){return false;}
        return $this->m->delete($name,$delay);
    }


    /**
     * @return mixed
     */
    public function clear()
    {
        if(!$this->have_extension){return false;}
        return $this->m->flush();
    }


    public function detail()
    {
        if(!$this->have_extension){return null;}
        return $this->m->info();
    }



}
```